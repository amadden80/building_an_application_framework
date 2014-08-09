# Building an Web App Framework (BAWAF) Part 1: Procedurally Generating Markup

## Introduction:

Web applications involve procedurally generated HTML.  There are not legions of developers editing your Twitter feed by hand.  This HTML is the product of computer logic running on the server side (and increasingly the client side).

## Problem statement 1:

Given any ruby string, how can I produce the following markup:

```html
<h1>[THE STRING]</h1>
```
---

## Problem statement 2:

Given the following array:

```ruby
  the_beatles = ['Ringo', 'George', 'Paul', 'John']
```

How can I procedurally generate the following markup:

```html
<ul>
  <li>Ringo</li>
  <li>George</li>
  <li>Paul</li>
  <li>John</li>
</ul>

```
---

##Problem statement 3:

Given the following array:

```ruby
  the_beatles = ['Ringo', 'George', 'Paul', 'John']
```

How can I write the below markup to a file `beatles.html`?

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
</head>
<body>
  <ul>
    <li>Ringo</li>
    <li>George</li>
    <li>Paul</li>
    <li>John</li>
  </ul>
</body>
</html>
```

---

##Problem statement 4:

Write erb templates in a new directory
A call to render prints the rendered template

---
## Relevant Notions and Softwares
- [ERB](http://ruby-doc.org/stdlib-2.1.2/libdoc/erb/rdoc/ERB.html)
- [File I/0](http://www.ruby-doc.org/core-2.1.2/File.html)
- Consider defining a ruby class with the following structures

``` ruby
  class HtmlBuilder

    def initialize(filename)
      # Save the filename for which the builder should write to
    end

    def h1(string)
      # STEP 1
        # Takes a string and produces a string inside of an h1 tag.
        # Eventually, it writes that string to a file.
    end

    def ul(items)
      # STEP 2
        # Take an array of items and returns a ul with lis for each item.
        # Eventually, it writes string to a file.
    end

    def render(filename)
      # STEP 4
        # Take, read, and render a template file[name]
        # Eventually, it writes string to a file.
    end

    private

    def layout
      # STEP 3
        # Returns boilerplate html inside of which additional markdown can be rendered.
    end

    def print(html_string)
      # Writes the contents of html_string to a file
    end

  end
```
