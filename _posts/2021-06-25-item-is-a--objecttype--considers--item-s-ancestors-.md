---
layout: post
title: item.is_a?(ObjectType) vs evaluating class
description:
date: 2021-06-25 07:27:00
image:
categories: ruby rails
tags: []
---

Given these classes

    class PaymentOrder
    end

    class StandalonePaymentOrder < PaymentOrder
    end

    class Another
    end

Careful with this refactor from

    item.is_a?(PaymentOrder) ? option_1 : option_2

to

    [PaymentOrder, Another].include?(item.class) ? option_1 : option_2

It's buggy

    StandalonePaymentOrder.last.is_a?PaymentOrder
      StandalonePaymentOrder Load (0.4ms)  SELECT `payment_orders`.* FROM `payment_orders` WHERE `payment_orders`.`type` IN ('StandalonePaymentOrder') ORDER BY `payment_orders`.`id` DESC LIMIT 1
    => true

but

    [PaymentOrder].include?(StandalonePaymentOrder.last.class)
      StandalonePaymentOrder Load (0.4ms)  SELECT `payment_orders`.* FROM `payment_orders` WHERE `payment_orders`.`type` IN ('StandalonePaymentOrder') ORDER BY `payment_orders`.`id` DESC LIMIT 1
    => false

So the correct refactor is

    [PaymentOrder, StandalonePaymentOrder, Another].include?(item.class) ? option_1 : option_2
