---
layout: post
title: Bash declaring variables
description: 
date: 2021-02-01 09:21:00
image: 
categories: bash
tags: []
---


`${VAR=value}` Assigns a value to the variable if it hasn't any and returns the value.  

    $ ${VAR=value}
    bash: value: command not found

The shell will try to execute it. If that is not you want o to avoid `bash: value: command not found` use the no-op operator `:`, which is part of the [Shell builtin commands](http://www.gnu.org/savannah-checkouts/gnu/bash/manual/bash.html#Bourne-Shell-Builtins){:target="_blank"}

Example

    $ echo $STH

    $ : ${STH=something}
    $ echo $STH
    something
    $ : ${STH=something_else}
    $ echo $STH
    something
