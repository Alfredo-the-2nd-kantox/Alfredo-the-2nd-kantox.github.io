---
layout: post
title: How to create a new Rails6 & Ruby2.7 application on MacOs BigSur
description: 
date: 2021-04-24 5:53:00
image: 
categories: ruby rails
tags: []
---

Instal Ruby (it takes a long time)

    asdf install ruby 3.0.0-preview1
    Downloading openssl-1.1.1g.tar.gz...
    -> https://dqw8nmjcqpjn7.cloudfront.net/ddb04774f1e32f0c49751e21b67216ac87852ceb056b75209af2443400636d46
    Installing openssl-1.1.1g...
    Installed openssl-1.1.1g to /Users/alfredoroca/.asdf/installs/ruby/3.0.0-preview1

    Downloading ruby-3.0.0-preview1.tar.bz2...
    -> https://cache.ruby-lang.org/pub/ruby/3.0/ruby-3.0.0-preview1.tar.bz2
    Installing ruby-3.0.0-preview1...
    ruby-build: using readline from homebrew
    Installed ruby-3.0.0-preview1 to /Users/alfredoroca/.asdf/installs/ruby/3.0.0-preview1

ATM not possible to detect Rails 6 with this Ruby version -> changed to Ruby 2.7.2



Start PostgreSQL & Adminer stack container

    #docker-compose.yml
    version: "3.7"
    services:
      postgres:
        image: postgres:13.0-alpine
        restart: always
        ports:
          - 5432:5432
        environment:
          POSTGRES_USER: postgres
          POSTGRES_PASSWORD: postgres
    adminer:
      image: adminer
      ports:
        - 8081:8080

Inside a temporary folder, install Rails

    echo "legacy_version_file = yes" >> ~/.asdfrc

    asdf plugin add nodejs
    asdf plugin add yarn
    asdf install nodejs latest
    asdf install yarn latest
    asdf global nodejs 15.6.0
    asdf global yarn

    node -v
    => v15.6.0
    yarn -v
    => 1.22.10

    #.tool-versions
    ruby 2.7.2

    gem install rails
    =>
    ...
    Successfully installed rails-6.1.3.1

    ruby -v
    => ruby 2.7.2p137 (2020-10-01 revision 5445e04352) [x86_64-darwin18]
    rails -v
    => Rails 6.1.3.1

Install PostgreSQL

    brew install postgresql
    ==> postgresql
    To migrate existing data from a previous major version of PostgreSQL run:
      brew postgresql-upgrade-database

    This formula has created a default database cluster with:
      initdb --locale=C -E UTF-8 /usr/local/var/postgres
    For more details, read:
      https://www.postgresql.org/docs/13/app-initdb.html

    To have launchd start postgresql now and restart at login:
      brew services start postgresql
    Or, if you don't want/need a background service you can just run:
      pg_ctl -D /usr/local/var/postgres start
      
Create new application

    rails new flashcards -d postgresql --webpack=stimulus

Comment line of gem pg in Gemfile

    bundle install
    bundle binstubs bundler
    rails webpacker:install
    ✨  Done in 22.60s.
    Webpacker successfully installed 🎉 🍰
 ->    rails webpacker:install:stimulus

Credentials -> NOT WORKING

    bin/rails credentials:edit --environment test

From here, the rails usual development: gems, generators, tests, ...
