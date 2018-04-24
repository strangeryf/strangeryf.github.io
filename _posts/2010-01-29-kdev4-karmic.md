---
layout: post
title:  "Kdevelop4 and Karmic"
date:   2010-01-29
tags: kdevelop ubuntu Linux
---
Ubuntu released Karmic (9.10) last October. Kdevelop4 was shipped with this release. However, it was 3.9.95 (beta5) at that time and was buggy and unstable as a result:

+ Project files for Kdevelop3 were not fully supported
+ Valgrind was not supported as expected
+ Debugging did not work

However, the new code browser was very impressive. After a quick search, I found the beta7 walkthrough from [Dr. Danz’ blog](http://blogs.fsfe.org/drdanz/?p=110). That is version 3.9.97, a somewhat usable version, which means most project creating, building, debugging and installing are supported.

The code browser is even better than Source Insight:

+ Hover to highlight
+ **Code Browser** window gives definition of select word, as well as its container, access, kind and declared location
![img]({{ '/assets/images/kdev4.png' | relative_url }}){: .center-image }

+ Hover and hint when **Code Browser** window not activated
![img]({{ '/assets/images/kdev4_hover.png' | relative_url }}){: .center-image }
