---
layout: post
title: If you ever need openssl v1.1...
description: 
date: 2021-01-23 18:17:00
image: 
categories: openssl macos
tags: []
---

If you need to have openssl@1.1 first in your PATH run:
  
    echo 'export PATH="/usr/local/opt/openssl@1.1/bin:$PATH"' >> /Users/alfredoroca/.bash_profile

For compilers to find openssl@1.1 you may need to set:

    export LDFLAGS="-L/usr/local/opt/openssl@1.1/lib"
    export CPPFLAGS="-I/usr/local/opt/openssl@1.1/include"

For pkg-config to find openssl@1.1 you may need to set:

    export PKG_CONFIG_PATH="/usr/local/opt/openssl@1.1/lib/pkgconfig"