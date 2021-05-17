---
layout: post
title: Echoing shell with linux script command
description: 
date: 2021-05-17 10:49:00
image: 
categories: []
tags: [linux]
---

Source: https://man7.org/linux/man-pages/man1/script.1.html


       -f, --flush
              Flush output after each write.  This is nice for
              telecooperation: one person does `mkfifo foo; script -f
              foo', and another can supervise in real-time what is being
              done using `cat foo'.  Note that flush has an impact on
              performance; it's possible to use SIGUSR1 to flush logs on
              demand.


Terminal 1:

    mkfifo foo; script -f foo

Terminal 2:

    cat foo
