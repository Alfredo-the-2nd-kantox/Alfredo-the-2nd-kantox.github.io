---
layout: post
title: "How to test printing output in Rspec"
date: 2021-08-25T09:07:25+02:00
categories: rspec
summary: Use `output` rspec matcher to check the result of `puts`
---

    def recently_published_books
      puts "==== Recently Published Books ===="
      puts "1. Atomic Habits"
      puts "2. Intelligent Investor"
    end


    it "should display the recently published books" do
      msg = <<-PUBLISHED.lines.map(&:strip).join("\n")
        ==== Recently Published Books ====
        1. Atomic Habits
        2. Intelligent Investor\n
      PUBLISHED

      expect { recently_published_books }.to output(msg).to_stdout
    end
