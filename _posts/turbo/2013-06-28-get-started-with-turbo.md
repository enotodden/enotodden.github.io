---
layout: post
category : turbo
tagline: 
tags : [turbo]
summary: >
    A collection of simple examples to get started with the blazing fast Turbo web framework.

---

The [Turbo](https://github.com/kernelsauce/turbo) web framework is really exciting, but since it's new and under heavy
development it lacks the documentation and Q&A resources of more established
projects. So I thought I'd do a writeup on how to get going with it.

<div class="alert">
    <strong>NOTE:</strong> Since Turbo is new and under heavy development, the contents of this
    tutorial might become outdated quickly. I'll try to update this to comply with the latest version.
</div>

I'm assuming that you know the Lua language and that you are that you have used an 
event-driven web solution before (Tornado, Node.js, etc.).

## What is Turbo?

In one (slightly long) sentence: [Turbo](https://github.com/kernelsauce/turbo) is a fast, elegant, open source (Apache 2.0) web framework built for LuaJIT with an API
modelled after Facebook's [Tornado](http://tornadoweb.org) web framework.

Developers description:
> Turbo Web is a Lua module / toolkit (whatever) for developing web apps in Lua. 
> It is different from all the other Lua HTTP servers out there in that it's modern, 
> fresh, object oriented and easy to modify,
> and probably the fastest scriptable Web server available. 


## Installing Turbo

First off, we need to install Turbo. Turbo needs LuaJIT to run, because it
uses the LuaJIT FFI features it will not run on 'official/normal/vanilla' Lua. 

### Getting LuaJIT
You can get the latest stable LuaJIT [here](http://luajit.org/download.html).
I'm not going to cover building and installing LuaJIT here, since it's documented
elsewhere. There's also apt-get'able packages on some distros.

### Getting and building Turbo

    $ git clone https://github.com/kernelsauce/turbo.git 
    $ cd turbo
    $ make install

Alternatively, you can also install turbo to a different place than /usr/local
by specifying TURBO\_PREFIX.

    $ make install PREFIX=/path/to/my/dir

### Alternative installation using turbo-virtual-env

If you want to install Turbo and LuaJIT in a self-contained directory
to avoid modifying system-wide stuff, you can use my [turbo-virtual-env](https://github.com/enotodden/turbo-virtual-env) script.

This will install everything in the directory passed to the `--create` parameter.

    $ cd /some/dir
    $ curl https://raw.github.com/enotodden/turbo-virtual-env/master/turbo-virtual-env | bash -s - --create ./env

To start using the newly installed LuaJIT and Turbo, just source the 'activate' script located in /some/dir/env/bin/activate
    
    $ . env/bin/activate

<hr>

Now that we have Turbo installed, it's time to go through some examples..

## Hello World 

The mandatory 'Hello World'.

<script src="https://gist.github.com/enotodden/5888700.js">
</script>

Explanation:

- Create a class to handle HTTP requests
- Define a method 'get' on that class to handle... GET requests..
  This method just sends the string 'Hello World!' to the client.
- Create an Application object, and assign the handler class to the route /hello
- Set the port to 8888 and start the server.

Usage and output:

<pre>
$ LuaJIT helloworld.lua
</pre>
<pre>
$ curl localhost:8888/hello
Hello World!
</pre>


## Request parameters

A slightly more advanced example, a server echoing the request parameter 'name'.

<script src="https://gist.github.com/enotodden/5893202.js">
</script>

Explanation:

- Same boilerplate as in the 'Hello World' example
- Get the 'name' parameter from the query string or request body and supply a default name
  if no 'name' parameter is found.
- Send 'Hello \[name\]!' to the client.

Usage and output:

<pre>
$ LuaJIT hello_name.lua
</pre>
<pre>
$ curl 'localhost:8888/hello?name=Espen'
Hello Espen!
</pre>
<pre>
$ curl localhost:8888/hello
Hello Santa Claus!
</pre>
<pre>
$ curl -X POST localhost:8888/hello -d name=Espen
Hello Espen!
</pre>
<pre>
$ curl -X POST localhost:8888/hello
Hello Easter Bunny!
</pre>

## Routes

As you can see in the above examples, Turbo has a routing feature.

You can assign handler classes to routes in the turbo.web.Application constructor.

Lua patterns can also be used for routing.

<script src="https://gist.github.com/enotodden/5896849.js">
</script>

## Serving Static Files

At least for development purposes, it's often useful to be able to serve static
assets. 

Turbo makes this really easy with the built in turbo.web.StaticFileHandler.

<script src="https://gist.github.com/enotodden/5896926.js">
</script>

## JSON Output

One nice feature of Turbo is implicit JSON conversion.

This means that you can pass a JSON-serializable table to self:write and
Turbo will set the 'Content-Type' header to 'application/json' and
serialize the table for you.

<script src="https://gist.github.com/enotodden/5893238.js">
</script>

<br>

That's it for now. I'll update this post with more stuff later on.

<br>
Changelog:
+ Changed `TURBO_PREFIX` to `PREFIX` since this was changed in commit `b6008de2b7f9228b2362b988a4f3c54d5bf4d11e`
+ Added alternative installation instructions using turbo-virtual-env
