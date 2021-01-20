---
layout: post
title: SQL Dump of currency_data 
description: 
date: 2021-01-17 05:42:00
image: 
categories: mysql
tags: []
---

    mysqldump -h 127.0.0.1 -u root -p secret --skip-add-drop-table --no-create-info --replace --extended-insert=FALSE kantoxflow currency_data > currency_data.sql