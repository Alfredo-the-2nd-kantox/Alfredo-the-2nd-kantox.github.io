---
layout: post
title: ZSH tips and tricks
description: 
date: 2021-03-10 05:41:00
image: 
categories: zsh bash
tags: []
---

source: https://dev.to/twilio/zsh-tricks-to-blow-your-mind-291f

Create and move to the new folder with `take`

    take = mkdir & cd

Mass rename files with `zmv`. To install zmv, run `autoload zmv`. An alternative to bash `rename`

    zmv -n '(*).(jpg|jpeg)' 'epcot-$1.$2'

Perform calculations from the command line with `zcalc`. An alternative to bash `bc`

`zsh-autosuggestions` suggests commands while you type according to your history of previous commands and completions.

`web-search` lets you open a search engine from your command line: running `google ___` will search Google for the given phrase

git plugin: https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/git

TBC Park a command. `Ctrl-q` "parks" the command you're currently typing and takes you back to the prompt, letting you start over and type another command. Once you run that other command, the original command is un-parked and refills the command line so you can continue--this is good for if you, say, forgot to do a command before a command.

Easily edit a command after you've typed it on the command line. If you've typed or pasted a long command and decide you need to edit it before running, `ctrl-x-e` opens it in an editor (usually vi, but you can set it to be any text editor with the $EDITOR environment variable.)

**oh-my-zsh Cheatsheet:** https://github.com/ohmyzsh/ohmyzsh/wiki/Cheatsheet

**zsh plugins:** https://github.com/unixorn/awesome-zsh-plugins
