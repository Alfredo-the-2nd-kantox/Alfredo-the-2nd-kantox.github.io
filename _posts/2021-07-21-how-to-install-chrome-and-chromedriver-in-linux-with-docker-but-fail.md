---
layout: post
title: How to install chrome and chromedriver in linux with docker but fail
description:
date: 2021-07-21 06:44:00
image:
categories: chrome docker linux
tags: []
---

# source: https://sites.google.com/a/chromium.org/chromedriver/downloads/version-selection

    RUN FULL_CHROME_VERSION=`curl -sS https://chromedriver.storage.googleapis.com/LATEST_RELEASE` && \
        # => 91.0.4472.101
        LAST_STABLE_CHROME_VERSION=${FULL_CHROME_VERSION%.*} && \
        # => 91.0.4472
        CHROMEDRIVER_VERSION=`curl -sS https://chromedriver.storage.googleapis.com/LATEST_RELEASE_$LAST_STABLE_CHROME_VERSION` && \
        # => 91.0.4472.101
        curl -o /tmp/chromedriver_linux64.zip https://chromedriver.storage.googleapis.com/index.html?path=$CHROMEDRIVER_VERSION && \
        mkdir -p /opt/chromedriver-$CHROMEDRIVER_VERSION && \
        unzip -qq /tmp/chromedriver_linux64.zip -d /opt/chromedriver-$CHROMEDRIVER_VERSION && \
        rm /tmp/chromedriver_linux64.zip && \
        chmod +x /opt/chromedriver-$CHROMEDRIVER_VERSION/chromedriver && \
        ln -fs /opt/chromedriver-$CHROMEDRIVER_VERSION/chromedriver /usr/local/bin/chromedriver

The line `unzip` fails with

    [/tmp/chromedriver_linux64.zip]

        End-of-central-directory signature not found.  Either this file is not
        a zipfile, or it constitutes one disk of a multi-part archive.  In the
        latter case the central directory and zipfile comment will be found on
        the last disk(s) of this archive.
      unzip:  cannot find zipfile directory in one of /tmp/chromedriver_linux64.zip or
              /tmp/chromedriver_linux64.zip.zip, and cannot find /tmp/chromedriver_linux64.zip.ZIP, period.

Tried repairing it with no success

    root@85f754e1906c:/src# zip -FF /tmp/chromedriver_linux64.zip --out /tmp/chromedriver_linux64-repaired.zip
    Fix archive (-FF) - salvage what can
      zip warning: Missing end (EOCDR) signature - either this archive
                        is not readable or the end is damaged
    Is this a single-disk archive?  (y/n): y
      Assuming single-disk archive
    Scanning for entries...
      zip warning: zip file empty
    root@85f754e1906c:/src# ls -al /tmp
    total 28
    drwxrwxrwt 1 root root  4096 Jul 21 07:16 .
    drwxr-xr-x 1 root root  4096 Jul 21 07:03 ..
    -rw------- 1 root root    22 Jul 21 07:16 chromedriver_linux64-repaired.zip
    -rw-r--r-- 1 root root 10574 Jul 21 07:10 chromedriver_linux64.zip
    drwx------ 2 root root  4096 Jul 20 09:53 tmp.Hy6hMEBIE8
    Note: this instruction comes from a Dockerfile
