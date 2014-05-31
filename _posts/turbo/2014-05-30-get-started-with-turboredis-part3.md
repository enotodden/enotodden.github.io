---
layout: post
category : turbo
title: "TurboRedis By Example - Part 3: 'PubSub'"
tagline: 
tags : [turbo, redis, turboredis]
summary: >
    A getting started tutorial for TurboRedis. Part 3.

---

*This is part 3 of the 'TurboRedis By Example' tutorial. I recommend
reading [part 1](/turbo/2014/05/26/get-started-with-turboredis-part1/) and
[part 2](/turbo/2014/05/26/get-started-with-turboredis-part2/) if you haven't done so yet.*

In the previous posts I've shown examples of how to use TurboRedis for 'normal'
Redis commands, and this time we'll be looking at Publish/Subscribe.

If you haven't used PubSub in Redis before, I recommend looking at [http://redis.io/topics/pubsub]() first.

In this example, we'll create a simple publisher application that broadcasts user input
from an HTTP GET request, through Redis, to a subscriber application.
The publisher will also submit a 'heartbeat' once in a while to let the subscribers
know it's still alive.

## The Publisher:
<script src="https://gist.github.com/enotodden/b9ebec7b367018b88f7c.js">
</script>

## The Subscriber:

*Note that this is using `turboredis.PubSubConnection` instead of `turboredis.Connection`*
<script src="https://gist.github.com/enotodden/307ad6dc6ba3e8b05532.js">
</script>


### Shell script for testing:
A shell script for posting messages to the publisher with curl every 2 seconds:
<script src="https://gist.github.com/enotodden/51423f0cf1a97f868f43.js">
</script>

---------------------

Things to take away:

- `PUBLISH` is just another command to TurboRedis.
- Only a `PubSubConnection` instance can be used to subscribe.
- A `PubSubConnection` instance can be used as any other connection until `:start()` is
  called. After this, only subscribe/unsubscribe commands are allowed.
- Subscribing is not wrapped/abstracted in any fancy way like it is in some
  other Redis clients. 
  Since it's not, no subscription verification is done by TurboRedis.
  You'll have to do approriate subscribe/unsubscribe message-handling yourself
  if you need it.


--------------------

This is the final post for now. I'll write a post on pipelining when the pipeline
feature is ready (or at least merged into the master branch).
