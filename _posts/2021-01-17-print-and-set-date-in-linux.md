---
layout: post
title: Print and set date in linux
description: 
date: 2021-01-17 05:42:00
image: 
categories: bash linux
tags: []
---

Print date

    for((;;)); do clear && date; done


Set date

    sudo date --set="2021-01-01 10:05:59.990"

Better way to update a server is

    sudo date -s "$(wget -qSO- --max-redirect=0 google.com 2>&1 | grep Date: | cut -d' ' -f5-8)Z"