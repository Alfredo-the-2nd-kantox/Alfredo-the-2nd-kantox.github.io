---
layout: post
title: "How to autocorrect Rubocop FactoryBot AttributeDefinedStatically"
date: 2021-08-25T07:49:33+02:00
categories: rubocop rspec
summary: Rubocop autocorrection capability
---

    bin/rubocop --require rubocop-rspec --only FactoryBot/AttributeDefinedStatically --auto-correct spec/factories/factories.rb

    # bad
    kind [:active, :rejected].sample

    # good
    kind { [:active, :rejected].sample }

    # bad
    closed_at 1.day.from_now

    # good
    closed_at { 1.day.from_now }

    # bad
    count 1

    # good
    count { 1 }
