---
layout: post
title:  "Strange header file"
date:   2006-02-27
tags: C++
---
In Visual C++, functions in a c file used by a cpp file should be declared with [extern "C"] in a header file. As a result, the c file should not include the header file, or you will recevie [error C2059: syntax error : 'string']. Fuctions in a cpp file used by another cpp file may skip that extern something. However, gcc will refuse to recognize that externed c function, so you have to use the _MSC_VER and __GNUC__ macro to detect the two different complier.