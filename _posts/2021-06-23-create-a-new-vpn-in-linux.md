---
layout: post
title: Create a new VPN in Linux
description:
date: 2021-06-23 12:46:00
image:
categories: linux vpn
tags: []
---

It needs `sudo` privileges, if no root user login use the command line

    sudo nm-connection-editor

To open the tunnel

    cd /path/to/config/file && sudo openvpn /path/to/config/file

To store the key password in a file

Create a file pass.txt with the password in one line and

    sudo chmod 600 pass.txt

To the vpn config file add the following

    askpass pass.txt

To open it daemonized add to the config file

    daemon
