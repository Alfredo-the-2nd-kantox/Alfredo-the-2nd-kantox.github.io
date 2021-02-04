---
layout: post
title: How to list databases and tables in Mysql
description: 
date: 2021-02-04 09:52:00
image: 
categories: mysql
tags: []
---

    mysql -h $ARCHIVE_DATABASE_HOST -p$ARCHIVE_DATABASE_PASSWORD $ARCHIVE_DATABASE_NAME -e "show databases;use archive; show tables;"

    +--------------------+
    | Database           |
    +--------------------+
    | information_schema |
    | archive            |
    | archive_test       |
    | #mysql50#ca.pem    |
    | mysql              |
    | performance_schema |
    +--------------------+
    +-------------------+
    | Tables_in_archive |
    +-------------------+
    | archived_versions |
    +-------------------+