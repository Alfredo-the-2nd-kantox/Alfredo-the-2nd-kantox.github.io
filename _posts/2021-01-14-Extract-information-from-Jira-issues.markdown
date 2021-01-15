---
layout: post
title:  "Extract information from Jira issues"
date:   2021-01-14 19:37:57 +0100
categories: jira
---

Each request has a test section where to put JS code to evaluate the response.

I used that feature to extract information from a Jira issue and print it to the Postman console.

This is the request:

    curl --location --request GET 'https://kantox.atlassian.net/rest/api/3//issue/RE-259/?fields=issuelinks' \
    --header 'Authorization: Basic YWxmcmVkby5yb2NhQGthbnRveC5jb206VDNQY3ZTaXI4T0JtdDNTZFk1YXY2QjJG' \
    --header 'Cookie: atlassian.xsrf.token=B26O-2I07-XP9H-9WAK_3b20322b3f580ac153ad6bcab824dff908dd67d3_lin'

This is the code in the tests:

    var responseJSON = pm.response.json();
    var res = responseJSON.fields.issuelinks;
    // console.log(res);
    for (const f of res) {
        if(f.outwardIssue) {
            console.log(f.outwardIssue.fields.issuetype.name + ": " + f.outwardIssue.key + " - " + f.outwardIssue.fields.summary + " - https://kantox.atlassian.net/browse/" + f.outwardIssue.key);
        }
    }

Note:

To create an Jira API token, connect to your account and go to: https://id.atlassian.com/manage-profile/security/api-tokens
Use it in the Authorization section in Postman to create the Basic Authorization credentials with you Jira email

For example (truncated)

    GET https://kantox.atlassian.net/rest/api/3//issue/RE-259/?fields=issuelinks

    Bug: EN-387 - Check that all the mailers properly use `I18n` - https://kantox.atlassian.net/browse/EN-387
    Bug: PT-5645 - AdminReadOnly is able to perform mutation operations - https://kantox.atlassian.net/browse/PT-5645
    Bug: PT-5773 - Excessive TracePoint usage in kantox-roles - https://kantox.atlassian.net/browse/PT-5773
    Tech Debt: PT-5611 - Copy production version records to the archive database - https://kantox.atlassian.net/browse/PT-5611
    Tech Debt: PT-5778 - Use mysqldump 5.6 in kantox-flow Dockerfile - https://kantox.atlassian.net/browse/PT-5778
