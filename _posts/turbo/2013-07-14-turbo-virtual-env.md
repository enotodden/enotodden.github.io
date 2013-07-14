---
layout: post
category : turbo
title: turbo-virtual-env, virtual-env like script for developing Turbo applications
tagline: 
tags : [turbo]
summary: >
    A post showing off the turbo-virtual-env script.

---

In the Python world, we have a tool called [virtual-env](http://www.virtualenv.org) for creating self-contained
directories (aka virtual environments) with a python installation and package management.

I missed this when using Turbo, so I made a simple virtual-env tool for working
with Turbo and LuaJIT. 
Though not as powerful as the Python tool, it's more than enough to set up a 
development environment for developing Turbo applications (or just Lua applications with LuaJIT for that matter).

The script has it's own git repo at [https://github.com/enotodden/turbo-virtual-env](https://github.com/enotodden/turbo-virtual-env).

**Features**:
- Installs LuaJIT, Turbo and LuaRocks in a self-contained directory/virtual enviroment
- Creates an `activate` script like the one the Python tool has for sourcing in the shell.
- Optionally reads a 'requirements' file and passes each line to `luarocks install`
- Optional Turbo Development mode (`--turbo-dev`) that creates an environment to 
  work on the code from an existing Turbo source tree.

<br>

**Installation**:

    curl https://raw.github.com/enotodden/turbo-virtual-env/master/turbo-virtual-env > /some/where/in/PATH/turbo-virtual-env
    chmod +x /some/where/in/PATH/turbo-virtual-env


**Basic usage**:

    turbo-virtual-env --create /path/to/my/environment

<br>

**More real-world-like example**:

This example shows how to create a new virtual environment with turbo-virtual-env.
<script src="https://gist.github.com/enotodden/5994524.js">
</script>

