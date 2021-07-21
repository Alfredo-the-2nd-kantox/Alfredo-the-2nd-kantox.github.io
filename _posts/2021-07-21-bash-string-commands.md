---
layout: post
title: Bash string commands
description:
date: 2021-07-21 07:33:00
image:
categories: [bash]
tags: []
---

string length

    LONG_STRING='paquito el chocolatero'
    echo ${#LONG_STRING}
    => 22

remove starting characters upto a position

    pos=8
    echo ${LONG_STRING:pos}
    => el chocolatero

delete the shortest match of $substring from back of $string

    ${string%substring}

Example

    CHROME_VERSION=`curl -sS https://chromedriver.storage.googleapis.com/LATEST_RELEASE` # => 91.0.4472.101
    LAST_CHROME_VERSION=${CHROME_VERSION%.*} # => 91.0.4472
