---
layout: post
title: Start Rails console with "pry" disabled
description: 
date: 2021-03-09 16:00:00
image: 
categories: rails
tags: []
---

pry-rails gem loads pry as rails console. If you need to start an irb console, without pry do:

    DISABLE_PRY_RAILS=1 rails c

I used it when playing with the `workflow` gem in my app and wanted to check the `before_transition` code. 

`next` is also a pry command, so I got "Error: Cannot find local context. Did you use `binding.pry`?" at `next` line.

BTW, in this code, `next` exits the block and accepts the transition.

    class Pepe
      include Workflow

      workflow do
        state :idle do
          event :hi, transitions_to: :eo
        end
        state :eo do
          event :puf, transitions_to: :pufo
        end
        state :pufo do
          event :ciao, transitions_to: :ciao
        end
        state :ciao

        before_transition do |from, to, event|
          puts "reaching"
          next if to == :eo
          puts "arriving"
          next if to == :pufo
          puts "pre-halt"
          halt
          puts "al final no halt"
        end
      end
    end

    irb(main):108:0> p=Pepe.new
    => #<Pepe:0x0000000ae80968>
    irb(main):110:0> [p.idle?,p.eo?,p.pufo?,p.ciao?]
    => [true, false, false, false]
    irb(main):112:0> p.hi!
    reaching
    irb(main):114:0> p
    => #<Pepe:0x0000000ae80968 @halted_because=nil, @halted=false, @workflow_state="eo">
    irb(main):115:0> [p.idle?,p.eo?,p.pufo?,p.ciao?]
    => [false, true, false, false]
    irb(main):116:0> p.puf!
    reaching
    arriving
    => "pufo"
    irb(main):117:0> [p.idle?,p.eo?,p.pufo?,p.ciao?]
    => [false, false, true, false]
    irb(main):118:0> p.ciao!
    reaching
    arriving
    pre-halt
    al final no halt
    => false
    irb(main):119:0> p
    => #<Pepe:0x0000000ae80968 @halted_because=nil, @halted=true, @workflow_state="pufo">