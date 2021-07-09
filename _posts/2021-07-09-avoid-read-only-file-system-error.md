---
layout: post
title: Avoid 'Read only file system' error
description:
date: 2021-07-09 10:41:00
image:
categories: macos
tags: []
---

When we trying to modify system files on macOS, starting from Catalina, we will see the error Read-only file system.

Fix:

1 Boot into maCOS Recovery mode (Holding Command + R or Command + Shift + R while powering on the mac, when we see the Apple logo and the progress bar, release the buttons)

2 Bring up the terminal window (From the menu bar at the top of the screen Utilities -> Terminal)

3 Disable System Integrity Protection first

    csrutil disable

4 Restart

Source: https://dannyda.com/2021/03/17/how-to-fix-macos-read-only-file-system-cant-modify-change-system-files-on-macos/