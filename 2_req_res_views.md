# Introduction

We interact with web applications through the browser and the HTTP protocol.  Now that we have the ability to procedurally generate markup, how can we do so via browswer interaction / HTTP requests?

## Problem Statement 1

What is Rack?  

Write an application using nothing but Rack that responds to all HTTP requests with a plain text representation of the current time.

## Problem Statement 2

Given the following arrays:

```ruby
  BEATLES = %w(john paul george ringo yoko)
  STONES  = %w(mick, keith, ronnie, charlie)
```

An http get request to '/stones' should render the following html:
```html

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Playing Around with Rack</title>
</head>
<body>
  <h1></h1>
  <h1>The Rolling Stones</h1>

  <ul>

    <li>mick</li>

    <li>keith</li>

    <li>ronnie</li>

    <li>charlie</li>

  </ul>

</body>
</html>

```

An http get request to '/beatles' should render the following html:
```html


<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Playing Around with Rack</title>
</head>
<body>
  <h1>THIS IS RENDERED IN THE LAYOUT</h1>
  <h1>The Beatles</h1>

  <ul>

    <li>john</li>

    <li>paul</li>

    <li>george</li>

    <li>ringo</li>

    <li>yoko</li>

  </ul>

</body>
</html>

```

## Relevant notions and softwares
- [Rack](http://rack.github.io/)
