---
layout: post
title: "Populate an Array in Ruby"
date: 2021-08-24T08:42:46+02:00
categories: ruby
summary: How to fill an array in Ruby
---


One way could be

    content = []
    content << "1st element"
    ...

Another more elegant way would be

    [].tap do |content|
      content << "1st element"
      ...
    end
