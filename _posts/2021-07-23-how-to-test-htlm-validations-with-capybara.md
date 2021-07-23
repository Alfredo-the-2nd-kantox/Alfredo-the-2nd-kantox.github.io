---
layout: post
title: How to test HTLM validations with Capybara
description:
date: 2021-07-23 16:31:00
image:
categories: capybara
tags: []
---

    ...
    And('I input some data And post'){
      within('#new_lead') do
        fill_form({
          client_uid: @client.uid,
          email: @client.email,
          name: @client.name,
          surname: @client.surname
        })
        fill_in 'lead_telephone', with: ''
        click_button 'Submit'
      end
      wait_until_modern_loaded
      wait_until_ui_unblocked
    }
    Then('I should see error'){ |msg|
      message = page.find('#lead_telephone').native.attribute('validationMessage')
      expect(message).to eq 'Please fill out this field.'

      # also works
      expect(find('#lead_telephone')['validationMessage']).to eq 'Please fill out this field.'
    }
