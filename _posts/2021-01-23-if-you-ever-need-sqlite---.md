---
layout: post
title: If you ever need sqlite...
description: 
date: 2021-01-23 18:17:00
image: 
categories: sqlite macos
tags: []
---

sqlite is keg-only, which means it was not symlinked into /usr/local,
because macOS already provides this software and installing another version in
parallel can cause all kinds of trouble.

If you need to have sqlite first in your PATH run:

    echo 'export PATH="/usr/local/opt/sqlite/bin:$PATH"' >> /Users/alfredoroca/.bash_profile

For compilers to find sqlite you may need to set:

    export LDFLAGS="-L/usr/local/opt/sqlite/lib"
    export CPPFLAGS="-I/usr/local/opt/sqlite/include"

For pkg-config to find sqlite you may need to set:

    export PKG_CONFIG_PATH="/usr/local/opt/sqlite/lib/pkgconfig"
