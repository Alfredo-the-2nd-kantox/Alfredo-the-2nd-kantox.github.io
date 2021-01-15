---
layout: post
title:  "Kernel operators overwritting"
date:   2020-12-14 19:37:57 +0100
categories: elixir
---

Not recommended but Kernel operators can be overwritten

    defmodule PlusPlus do
      import Kernel, except: [++: 2]

      def a ++ b, do: [{a, b}]
      def keyword(arg1, arg2), do: arg1 ++ arg2
    end

    import PlusPlus

    PlusPlus.keyword(:foo, 42)

    #⇒ [foo: 42]

