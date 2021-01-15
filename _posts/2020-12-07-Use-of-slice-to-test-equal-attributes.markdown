---
layout: post
title:  "Use of `slice` to test equal attributes"
date:   2020-12-07 19:37:57 +0100
categories: ruby rspec
---


    attrs = %i[attribute_1 attribute_2 attribute_3]
    expect(object_1.attributes.slice(attrs)).to eq object_2.attributes.slice(attrs)

