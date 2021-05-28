---
layout: post
title: Execute code when RSpec scenario fails
description:
date: 2021-05-28 15:39:00
image:
categories: rails rspec
tags: []
---

To execute code if a test fails:

    # spec/spec_helper.rb

    after(:each) do |example|
      if example.exception
        # Print the test log or get more data
      end
    end
