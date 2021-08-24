---
layout: post
title: "Git fetch & rebase vs git pull"
categories: git
tags:
date: 2021-08-07
summary: Use Git effectively
---

It is recomended not pulling. Instead, do the following

	git fetch
	git rebase <upstream>/<branch>
