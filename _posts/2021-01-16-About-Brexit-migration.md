---
layout: post
title:  "About Brexit migrations"
date:   2021-01-16
categories: general
---

We create several rake tasks to do the client and trades novation. These are some thoughts:

- Try to keep transactions agile (short time and memory usage) with batches of few records
- Avoid usage of the word "client", it leads to confusion in Kantox. Proper naming is hard.
- In migrations, do not use conditional execution with "tables_exist?". Instead use `rake db:migrate:redo` or `VERSION=XYZ rake db:migrate:down && rake db:migrate`
- Prefer `pluck` against `select` in queries
- Use `find_in_batches` when dealing with a lot of records
- In rake tasks and tests, use `create!` and `save!` bang versions unless there is proper error handling code
- In rake tasks, report the number of successful records over the total number of processed records.
