---
layout: post
title: Find out which branch contains a change
description: 
date: 2021-01-17 05:42:00
image: 
categories: git
tags: tip
---

This filters the lists of branches to only those who have the given commit among their ancestors.

    $ git branch --contains 50f3754

Include the “-a” flag to also include remote-tracking branches in the list.