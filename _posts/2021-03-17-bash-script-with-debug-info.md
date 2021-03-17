---
layout: post
title: bash script with debug info
description: 
date: 2021-03-17 11:24:00
image: 
categories: [bash]
tags: []
---

With this piece, you can enable debuging by setting an ENV var

    if [[ "$DEBUG" == "1" ]] ; then
      set -x
    fi

    ...