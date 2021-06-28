---
layout: post
title: How to send mails after cron run
description:
date: 2021-06-27 07:27:00
image:
categories: linux
tags: []
---

Sources:
- https://www.cyberciti.biz/tips/linux-use-gmail-as-a-smarthost.html
- https://tecadmin.net/bash-mail-command-not-found/

Install mail service

    sudo yum install mailx

Install ssmpt

    yum install ssmtp

Configure gmail as smarthost

    vi /etc/ssmtp/ssmtp.conf

Update config

    # Use SSL/TLS to send secure messages to server.
    UseTLS=YES
    #IMPORTANT: The following line is mandatory for TLS authentication
    TLS_CA_File=/etc/pki/tls/certs/ca-bundle.crt

    AuthUser=gmail-user-email
    AuthPass=gmail-password
    FromLineOverride=YES
    mailhub=smtp.gmail.com:587
    UseSTARTTLS=YES

Also, make sure you disable Sendmail:

    service sendmail stop
    chkconfig sendmail off
    mkdir /root/.bakup
    mv /usr/sbin/sendmail /root/.bakup
    ln -s /usr/sbin/ssmtp /usr/sbin/sendmail

Test it

    echo "Message Body" | mail -s "Message Subject" receiver@example.com

Failed messages are placed in `dead.letter` in the sender’s home directory.

If mail is sending from the command line but not through crontab, try changing FromLineOverride to NO in `/etc/ssmtp/ssmtp.conf`.

You can also get more detailed logging by adding `Debug=YES` to `ssmtp.conf` - the extra logging goes to `/var/log/mail.log` or `/var/log/maillog`.

Ensure "Allow less secure apps"

https://www.google.com/settings/security/lesssecureapps

Unlock captcha

https://accounts.google.com/b/0/DisplayUnlockCaptcha

How to stop particular cronjob mails.

Add ` >/dev/null 2>&1` to the crontab line

Stop sending cron emails

    MAILTO= ""

How to customize email subject

Call the email command in the same crontab line by adding

    <cron job line> 2>&1 | mail -s $(date "+%Y%m%d-%H%M%S") example@gmail.com
