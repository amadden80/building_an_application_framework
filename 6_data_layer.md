## Introduction

Thus far we have had no way of persisting data or interacting with persisted data.  

Over the course of this lab, we will be developing our own version of ActiveRecord, `PassiveRecord`.

It will take advantage of ths pre-written adapter class.  

```ruby
class PostgresAdapter

  def initialize
    require "pg"
    @db = PG.connect( dbname: 'wdi_3000' ) #user must specify databse
  end

  def execute(sql)
    data = @db.exec(sql).map do |row|
      row.each_with_object({}){|(k,v), hash| hash[k.to_sym] = v} # symbolize keys
    end
  end

  def columns(table_name)
    @db.exec("SELECT column_name FROM information_schema.columns WHERE table_name='#{table_name}';").map do |row|
      row['column_name'].to_sym
    end
  end

end
```

Starter:

```ruby

module PassiveRecord
  class Base

    @@connection = PostgresAdapter.new

    def initialize(attributes = {})
      columns == @@connection.columns(self.class.table_name) # columns defined in our table
      attributes.keys.each { |attr| raise PassiveRecord::UnknownAttributeError.new(attr) unless columns.include?(attr) } # raise error of object instantiated with attributes misaligned to table columns
      @attributes = attributes #all attributes stored in single instance variable
    end

    def method_missing(*args)

      # This is fancy metaprogramming so that we don't need to write
      # instance methods for each attribute defined for a given class.
      # When we call `beatle.name`, for instance, method_missing will be called.
      # But rather than throw an error, it will capture the method name
      # and use it as a key to the objects attributes hash.  Importantly,
      # a call to super preserves the functionality of method_missing should
      # neither of our gaurd clauses be satisfied.

      return @attributes[args[0]].to_i if !@attributes[args[0]].to_i.zero? #returns integer if it can be parsed into int
      return @attributes[args[0]] if @attributes[args[0]]
      super
    end

    def self.table_name
      self.name.downcase+"s"
    end

    def save
      # saves resource to database and returns object with id attribute set.
    end

    def update(attributes)
      # updates specific attributes for a given resource.
    end

    def self.create(attributes={})
      # instantiates an object and saves to database
    end

    def self.delete(id)
      # deletes a specified resource from the database
    end

    def self.all
      # returns all records
    end

    def self.find(id)
      # finds a specfied record.  
      # Raises PassiveRecord::RecordNotFound error if
      # record not found.
    end

    def self.first

    end

    def self.last

    end
  end

  class UnknownAttributeError < NoMethodError
    def initialize(attribute)
      @attribute = attribute.to_s
      super("unknown attribute: #{attribute}")
    end
  end
end

```
## Things to keep in mind

- Should one be able to alter `created_at` and `id` columns?  Do we need to do anything to prevent this?

- Of what type of object are our records when they come back from the database?  Of what type should they be?
