---
layout: post
title: Sidekiq jobs and workers
description: 
date: 2021-01-17 05:42:00
image: 
categories: [sidekiq]
tags: []
---

We have a cron job that ensures another runs

    DynamicHedging::LinkDeferredEntriesJob.perform_in(1.seconds, true)

We want to run it if there isn't any job already enqueued nor running

So

    class LinkDeferredEntriesWatchdogJob
      include Sidekiq::Worker

      sidekiq_options retry: false

      def perform
        return if enqueued_jobs.count == 1 || there_are_busy_jobs?

        Kantox::Rescuer.logger.warn("DynamicHedging::LinkDeferredEntriesJob has [#{jobs.count}] running instances, restarting...")
        jobs.each(&:delete)

        DynamicHedging::LinkDeferredEntriesJob.perform_in(1.seconds, true)
      end

      def enqueued_jobs
        Sidekiq::Queue.all.flat_map do |queue|
          queue.select do |job|
            job.klass == 'DynamicHedging::LinkDeferredEntriesJob' &&
              job.args.first
          end
        end
      end

      def there_are_busy_jobs?
        Sidekiq::Workers.new.any? do |_process_id, _thread_id, work|
          work['payload']['class'] == 'DynamicHedging::LinkDeferredEntriesJob' && work['payload']['args'] == [true]
        end
      end
    end
