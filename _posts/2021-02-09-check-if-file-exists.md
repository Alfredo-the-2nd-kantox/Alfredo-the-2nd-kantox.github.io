---
layout: post
title: Check if a file exists and create it
description: 
date: 2021-02-09 17:41:00
image: 
categories: bash
tags: []
---

    #!/usr/bin/env bash
    FILE=some_file
    if [[ ! -f "$(pwd)/$FILE" ]]; then
      touch "$(pwd)/$FILE"
      echo "$(pwd)/$FILE created!"
    else
      echo "$(pwd)/$FILE"
      echo "$(pwd)/$FILE already exists!"
    fi

UPDATE:

No need to check if the file exists; `touch` will do it itself

    touch "$(pwd)/$FILE"

