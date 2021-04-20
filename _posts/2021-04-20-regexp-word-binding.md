---
layout: post
title: Regexp word binding
description: 
date: 2021-04-20 13:49:00
image: 
categories: regexp
tags: []
---

I want to hide sensitive information to the user that comes in the response.

For example, `sensitive_info` appears in the error details response. We want to log the real response but to hide the sensitive info in the response to the client. 

That info can be also part of a reference. In that case, it mustn't be changed, only if it is an independent word. For example, `LCL` is an LP and `O-XSLCLRTY` can be a reference. We want to hide it in `No response from LCL` but not inside the order's reference.
 
    def hide_sensitive_info(error_details, sensitive_info)
      word_binding = /\b/.source
      regexp = Regexp.new(word_binding + sensitive_info + word_binding, true)
      error_details.gsub(regexp, 'liquidity provider')
    end

See it in the code: https://github.com/kantox/kantox-flow/blob/master/app/controllers/api/v1/base_controller.rb
