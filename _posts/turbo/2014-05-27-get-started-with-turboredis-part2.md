---
layout: post
category : turbo
title: "Getting started with TurboRedis - Part 2: 'Caching GitHub API requests'"
tagline: 
tags : [turbo, redis, turboredis]
summary: >
    A getting started tutorial for TurboRedis. Part 2.

---

*This is part 2 of the 'Getting started with TurboRedis' tutorial, I recommend
reading [part 1]() if you haven't done so yet.*

We're back. And now that we have the boilerplate stuff done, it's time
for a more useful example.
This example is a little application that lists a GitHub user's repositories
in an HTML list.
It only uses a few basic Redis commands: `GET`, `TTL` and `SETEX`.

The list of repositories is retrieved from the public
GitHub API and the responses are cached in Redis for 10 seconds.
It will also print bold text under the repositories list indicating
wether it was a cache hit or a cache miss.
If it was a cache-hit, the remaining time-to-live for the Redis key
is also printed.

<script src="https://gist.github.com/enotodden/e58cef312e87b923be0e.js">
</script>

Things to take away from this example:

- Commands can be called with `corountine.yield()` (which uses `turbo.async.task`
   under the hood) or with traditional callbacks.
- TurboRedis auto-converts replies from many commands. In this example
   the time-to-live value is returned as an integer.
   This behaviour is somewhat inconsistent at the moment and can be
   disabled completely by passing `purist=true` to `turboredis.Connection:new()`.
- When using callbacks with TurboRedis you have to call `self:set_async(true)`
   in the RequestHandler to prevent Turbo from finishing the request
   before you intend to. This also means that you have to `:finish()` when
   the request is done.
-  Host and/or port can be passed to `turboredis.Connection:new()` in a table.
-  TurboRedis never touches arguments to commands, it only converts them to
   strings, so all command-functions uses the same argument order as described
   in the [Redis Command Reference](http://redis.io/commands).

That's it. Part 3 will be covering Publish/Subscribe.

If you're bored to death and have nothing else to do, or just want more examples,
you can check out the [Git Repo](https://github.com/enotodden/turboredis) or
the [TurboRedis docs](https://blog.puvoid.com/turboredis/).
