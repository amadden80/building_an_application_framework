## Introduction

By now, our application can handle basic HTTP GET and POST requests.  But our code is... pretty ugly.  It has big, ugly control flow statements and is not particularly object oriented.  It makes sense for us to develop an object that tells our application how to react when different types of requests come in.  

Enter the Router class.  


## Problem Statement 1

For now, we will remain concerned only with GET and POST requests.

A router should have a `create_route` method that takes an `HTTP verb`, a `path`, and a `block` of code as its arguments.  This block of code will be executed when the route is called. You will need to choose an appropriate data structure to store the block so that it can be easily accessed and called in response to its associated HTTP request.

## Problem Statement 2

A router should have a `process` method.  We leave it to you to determine what arguments it should take.  A call to this method should ultimately determine the HTTP Verb and Path associated with a request and call the block of code that corresponds to the request.  

## Problem Statement 3

What if we are requesting a particular resource?

Can our router appropriately handle a GET request to '/beatles/5' (i.e. a request for Stu Sutcliffe)?  We  mayneed to test this incoming path against some sort of regular expression to match it to the appropriate route.  
