---
layout: post
title:  "Windows Update froze"
date:   2006-02-21
tags: Windows
---
This monday, I found my PC froze when accessing Windows Update, and MSN messenger also froze after logging in.
After googling, I checked my log file and found the following records,
```
2006-02-18 15:17:20 1524 640 Shutdwn Install at shutdown: no updates to install
2006-02-18 15:17:20 1524 640 Shutdwn FATAL: WUCheckForUpdatesAtShutdown failed, hr=8024A000
......
2006-02-20 09:45:52 3260 cc0 DtaStor Update service properties: service registered with AU is {9482F4B4-E343-43B6-B170-9A65BC822C77}
2006-02-20 09:45:52 3260 cc0 DtaStor WARNING: Update Service: Failed to update backup store
```
It’s clear that the problem must have something to do with the DataStore folder and Download folder in %systemroot%\SoftwareDistribution. I could not delete them in normal state, and I had to reboot and entered safe mode, and successfully remove them. Windows Update became ok after a reboot, and so did MSN messenger.
