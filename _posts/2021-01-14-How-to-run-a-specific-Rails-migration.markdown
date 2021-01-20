---
layout: post
title:  "How to run a specific Rails migration"
date:   2021-01-14 19:37:57 +0100
categories: rails migration
---

    $ rails console
    irb(main)> require "#{Rails.root.to_s}/db/migrate/20160211142708_create_onboardings.rb"
    irb(main)> CreateOnboardings.migrate(:up)

Source: [https://www.firmhouse.com/blog/forcing-a-rails-database-migration](https://www.firmhouse.com/blog/forcing-a-rails-database-migration)
