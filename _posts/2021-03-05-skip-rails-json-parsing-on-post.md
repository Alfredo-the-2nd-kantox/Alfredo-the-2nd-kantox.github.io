---
layout: post
title: Skip Rails JSON parsing on POST
description: 
date: 2021-03-05 07:02:00
image: 
categories: []
tags: rails, json
---

When AppMap data is received by the AppLand server, we want to get it into PostgreSQL as fast as possible. When Rails receives an HTTP request with *content type* `application/json`, it parses the request JSON into Ruby objects and then passes this data, as `params`, to the controller. Since all we want to do is insert the data into PostgreSQL, and PostgreSQL can parse the JSON itself, we don’t need Rails to do any parsing. So, we disable Rails JSON parsing behavior by sending *content type* `multipart/mixed` instead of `application/json`. In this way, we minimize the amount of request processing that’s performed in the application tier. The JSON data is loaded efficiently into PostgreSQL, without having to sacrifice all the benefits provided by the Rails framework.

Source: https://dev.to/kgilpin/4-ways-to-accelerate-json-processing-with-rails-and-postgresql-nfa