---
layout: post
title: Rspec matchers for response statuses
description: 
date: 2021-04-24 20:53:00
image: 
categories: rspec
tags: []
---

    response.methods.grep(/\?/)
    =>
    [:sending?,
    :sent?,
    :committed?,
    :has_header?,
    :mon_locked?,
    :mon_owned?,
    :last_modified?,
    :date?,
    :etag?,
    :weak_etag?,
    :strong_etag?,
    :redirection?,
    :invalid?,
    :redirect?,
    :include?,
    :informational?,
    :client_error?,
    :ok?,
    :created?,
    :accepted?,
    :no_content?,
    :moved_permanently?,
    :bad_request?,
    :unauthorized?,
    :forbidden?,
    :precondition_failed?,
    :unprocessable?,
    :method_not_allowed?,
    :not_found?,
    :successful?,
    :server_error?,
    :duplicable?,
    :html_safe?,
    :in?,
    :present?,
    :blank?,
    :acts_like?,
    :tainted?,
    :untrusted?,
    :frozen?,
    :instance_variable_defined?,
    :instance_of?,
    :kind_of?,
    :is_a?,
    :nil?,
    :eql?,
    :respond_to?,
    :equal?]