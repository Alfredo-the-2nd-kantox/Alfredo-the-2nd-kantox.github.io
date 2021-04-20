---
layout: post
title: Test configuration through ENV variable
description: 
date: 2021-04-20 10:53:00
image: 
categories: rspec rails
tags: []
---


**Explanation:**

ENV variables are read only once when the class/module is loaded.

Therefore, it can not be mocekd or changed in tests.

The solution for testing goes through using methods that can be mocked, like `configured?`


    module FixRelay
      module Api
        # Ruby client to communicate with Fix-relay via Http
        class Publish
          include HTTParty
          BASE_ENDPOINT = ENV.fetch('FIX_RELAY_URL') { '' }

          base_uri BASE_ENDPOINT

          ...

          def self.configured?
            BASE_ENDPOINT.present?
          end

          def self.ensure_configured!
            return if configured?

            # manage error
            error = 'FIX_RELAY_URL not set. Requests for best price are going to fail!'
            Kantox::Rescuer.log_error(error).airbrake
            raise Kantox::Exceptions::StandardError.new, error
          end
        end
      end
    end


    # spec in class which uses FixRelay::Api::Publish

    context 'when FixRelay endpoint has not been configured' do
      before { flexmock(FixRelay::Api::Publish, configured?: false) }

      it 'raises and airbrakes the error' do
        flexmock(Kantox::Rescuer).should_receive('log_error.airbrake').once

        expect { subject.issue_market_trade(order) }.to raise_error Kantox::Exceptions::StandardError, /FIX_RELAY_URL/
      end
    end
