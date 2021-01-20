---
layout: post
title: Bash scripts special parameters
description: 
date: 2021-01-20 07:50:00
image: 
categories: bash
---

Source: [https://tiswww.case.edu/php/chet/bash/bashref.html#Special-Parameters](https://tiswww.case.edu/php/chet/bash/bashref.html#Special-Parameters)

($@) 

Expands to the positional parameters, starting from one. 

In contexts where word splitting is performed, this expands each positional parameter to a separate word; if not within double quotes, these words are subject to word splitting. 

In contexts where word splitting is not performed, this expands to a single word with each positional parameter separated by a space. 

When the expansion occurs within double quotes, and word splitting is performed, each parameter expands to a separate word. 

That is, "$@" is equivalent to "$1" "$2" ... 

If the double-quoted expansion occurs within a word, the expansion of the first parameter is joined with the beginning part of the original word, and the expansion of the last parameter is joined with the last part of the original word. When there are no positional parameters, "$@" and $@ expand to nothing (i.e., they are removed).

Example in kantox-flow docker_run.sh

    case "$@" in
      'prepare')        docker_prepare
                        docker_test_prepare
                        ;;
      'test:prepare')   docker_test_prepare
                        ;;
      'prepare_'*)      $@
                        ;;
      'shell'|'bash')   docker_prepare
                        docker_test_prepare
                        docker_run bash
                        ;;
      'bare_shell')     BARE_SHELL=1 docker_prepare
                        docker_run bash
                        ;;
      'sidekiq')        docker_prepare
                        docker_run bundle exec sidekiq
                        ;;
      'reset')          docker_reset
                        ;;
      *)                docker_prepare
                        docker_run $@
                        ;;
    esac
