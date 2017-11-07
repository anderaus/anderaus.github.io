---
title: "Schedule an Azure Function using local time"
date: 2017-11-07 22:14:00
categories:
  - troubleshooting
tags: 
  - azurefunctions
  - cron
  - timezones
---

I have an Azure function that needs to run at 07:00 in the morning and 15:00 in the afternoon every day - *Norwegian time*.

By default, the CRON expression used to schedule a time-triggered Azure function uses UTC. As Norway is UTC+1 I had set the CRON expression to:

<code>0 0 5,13 * * *</code>

This worked fine all the way through the winter, but when daylight savings kicked in (and Norway moves to UTC+2) the trigger was one hour off.

> Note: Azure Functions use a 6 value CRON expression on the form <code>{second} {minute} {hour} {day} {month} {day-of-week}</code>, not the regular 5-value CRONs without seconds.

Luckily, the CRON expression respects the time zone of the web app if specified using the `WEBSITE_TIME_ZONE` key:

![Website time zone setting](/images/171107_WebsiteTimeZoneSetting.PNG){: .align-center}

Valid values for time zones can be found [in this list](https://technet.microsoft.com/library/cc749073(v=ws.10).aspx).

After adding the setting in the Azure Portal I just needed to change my CRON expression to Norwegian hours; <code>0 0 7,15 * * *</code>, and everything worked fine.
