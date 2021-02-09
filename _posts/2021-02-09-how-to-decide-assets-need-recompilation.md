---
layout: post
title: How to decide if Rails assets need recompilation
description: 
date: 2021-02-09 13:23:00
image: 
categories: bash macos rails
tags: []
---

    if [[ "$(find app/assets/ -type f -print0 | xargs -0 stat -f '%Sm' -t '%s' | sort -rn | head -1)" > \
          "$(find public/assets/ -type f -print0 | xargs -0 stat -f '%Sm' -t '%s' | sort -rn | head -1)" ]]
    then
      log "Precompiling assets ..."
      docker_run "bundle exec rake assets:precompile --trace" || ( log_failure && exit 1 )
    else
      log "Assets up-to-date!"
    fi


This line gets the newest file date in numeric format

    find app/assets/ -type f -print0 | xargs -0 stat -f '%Sm' -t '%s' | sort -rn | head -1

References: [stat](https://ss64.com/bash/stat.html) [sort](https://ss64.com/osx/sort.html) [head](https://ss64.com/osx/head.html)