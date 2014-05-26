---
layout: post
category : turbo
title: "Getting started with TurboRedis - Part 1: 'Hello World'"
tagline: 
tags : [turbo, redis, turboredis]
summary: >
    A getting started tutorial for TurboRedis that walks through the essential
    steps of using TurboRedis in a Turbo-based web application.

---


In October I started writing a Redis library for Turbo, mostly for my own
personal use. But since then it has grown to be a pretty stable library, and
I thought it might be useful for others. I realize however that it's lacking
some documentation and some practical examples.

So I decided to do a 'Get Started' tutorial walking through the features
and use-cases of TurboRedis by example. I'll start off today with a simple
'Hello World' example and add more parts in the coming days.

### Prerequisites
- Basic understanding of Turbo and Redis.
- A LuaJIT and Turbo environment of some kind.
- Redis (I recommend the latest stable release) running on the default port.

If you want to learn more about Turbo or if you're just getting started with it,
I recommend having a look at the examples and tutorials at [http://turbolua.org]().

If you don't have an environment, and want to set one up really fast, I shamelessly
recommend my own turbo-virtual-env tool and my blog post showing how to
use it [here](/turbo/2013/07/14/turbo-virtual-env/).


## Hello (Turbo)Redis

This example should be self-explanatory, but I overcommented it just to
be sure.

We create a simple Turbo application with one handler that displays
the message 'Hello World!!!' and the number of visits since the
server was started the first time. 
Both of these values are set and retrieved from Redis.

The visit count persists as long as the key exists is in Redis, meaning
that it will start from where it was last time if you restart the server.

<script src="https://gist.github.com/enotodden/6badce365df637481efe.js">
</script>

That's it. Part 2 will be more practical showing how to use Redis to cache
GitHub API requests in a simple Turbo application.

If you're bored to death and have nothing else to do, or just want more examples,
you can check out the [Git Repo](https://github.com/enotodden/turboredis) or
the [TurboRedis docs](https://blog.puvoid.com/turboredis/).
