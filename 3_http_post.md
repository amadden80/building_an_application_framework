## Introduction

The HTTP protocol specifies that a client can make different types of request to a server.

Speaking generally, a GET request typically involves the client asking for a set of resources from the server.

A POST request, on the other hand, involves the client submission of form data to the server and the subsequent creation of a new resource.

There are other HTTP verbs, but let's not worry about them for now.

## Problem Statement 1

Examine the contents of the `env` hash that gets passed into the .call method of your Rack Application.  Is there any clue as to which type request is being made? In other words, what key corresponds to the HTTP Verb for a given request?

## Problem Statement 2

Add functionality to your application so that it is in accord with the following specification:

| HTTP Request | Behavior |
|------|-----|
| `GET '/beatles'`  `GET '/stones'`| Renders list of band members and a form with a single field with name="member" |
| `POST '/beatles'` `POST '/stones'`| Form data is pulled out of parameters and a new member is created (i.e. appended to the existing array).  HTML reflecting additional member is sent back to the client.  **NOTE:** Typically we do not render HTML from a post request but it is okay for the purpose of this exercise.  
