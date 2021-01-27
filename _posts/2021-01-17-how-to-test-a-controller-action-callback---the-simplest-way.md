---
layout: post
title: How to test a controller action callback - the simplest way
description: 
date: 2021-01-17 05:42:00
image: 
categories: rails test
tags: []
---

See it in action at `spec/controllers/api/v1/api_controller_spec.rb`

    context 'logging' do
        before do
          class ::TestingApiLoggingController < Api::V1::ApiController
            def hello
              render :nothing => true
            end
          end

          routes.draw do
            get 'hello' => 'testing_api_logging#hello'
          end

          @controller = TestingApiLoggingController.new
        end

        # important to leave things as they were before
        after do
          Object.send(:remove_const, :TestingApiLoggingController)
          Rails.application.reload_routes!
        end

        let(:api_log_entry) { Api::ApiLogEntry.new(index: 'api', connection: 'GET') }

        it 'should log' do
          flexmock(api_log_entry).should_receive(:log!).once
          flexmock(Api::ApiLogEntry).should_receive(:new).and_return(api_log_entry).once
          get :hello
        end
      end
    end