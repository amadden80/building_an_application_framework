## Introduction


## Problem Statement 1

How can we take advantage of our existing method to make our framework syntactically similar to Sinatra.  I'd like to be able to define routes as follows.  Consider defining a class method on an application class.

```ruby

class MyApp < Application
  get '/' do
    @beatles = ['john', 'paul', 'george', 'ringo', 'yoko']
  end
end

```

## Problem Statement 2

How can a access params from a given request inside of a block of code?

```ruby

class MyApp < Application
  get '/beatles/:id' do
    beatle = Beatle.find(param[:id])
  end
end

```
