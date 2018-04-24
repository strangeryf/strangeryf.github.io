---
layout: post
title:  "Some registry location in Windows 7"
date:   2011-01-17
tags: registry Windows
---
Microsoft has notorious habit of storing configurations in Windows registry. Usually you will find plain text, such as “run” history in
[HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\RunMRU]

But sometime, you will find encoded strings. For example, you can find these strange strings of image locactions in
[HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\Wallpapers\Images]

Anyway, lots of old tricks such as autorun, still work.
