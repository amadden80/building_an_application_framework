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

    def self.table_name
      self.name.downcase+"s"
    end

    def save
      # saves resource to database and returns object with id attribute set.
    end

    def update
      # 
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
