---
layout: post
title: Handle ENV vars in Rails
description: 
date: 2021-02-03 11:52:00
image: 
categories: rails env
tags: []
---

[DotEnv](https://github.com/bkeepers/dotenv) is a great Gem to handle ENV vars in a Rails application.

[Here](https://github.com/bkeepers/dotenv#what-other-env-files-can-i-use) there is a table that summarizes the different files where to put the variables. It is reproduced below.

TL;DR

- safe, default values in `.env.development`. This goes in the repo.
- custom overrides in `.env.development.local` or `.env.local`
- other vars nonrelated to the app itself in `.env`

## List of priorities

Hierarchy Priority | Filename | Environment | Should I .gitignoreit? | Notes
-------------------|----------|-------------|------------------------|------
1st (highest)|.env.development.local|Development|Yes!|Local overrides of environment-specific settings.
1st |.env.test.local|Test|Yes!|Local overrides of environment-specific settings.
1st |.env.production.local|Production|Yes!|	Local overrides of environment-specific settings.
2nd |	.env.local|	Wherever the file is|	Definitely.|	Local overrides. This file is loaded for all environments except test.
3rd |	.env.development|	Development|	No.|	Shared environment-specific settings
3rd |	.env.test|	Test|	No.|	Shared environment-specific settings
3rd |	.env.production|	Production|	No.|	Shared environment-specific settings
Last |	.env|	All Environments|	Depends (See below)|	The Original®