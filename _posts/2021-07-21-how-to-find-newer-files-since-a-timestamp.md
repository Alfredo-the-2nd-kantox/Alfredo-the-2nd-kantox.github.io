---
layout: post
title: How to find newer files since a timestamp
description:
date: 2021-07-21 08:01:00
image:
categories: [linux]
tags: []
---

Create a reference file to compare with

    touch -t yyyymmddhhmm timestamp

Find newer files

    find . -newer timestamp

And it can be passed to further commands

    find . -newer timestamp | xargs rspec
