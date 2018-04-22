---
layout: post
title:  "Stringification"
date:   2007-07-26
tags: c
---
ref: https://gcc.gnu.org/onlinedocs/gcc-3.4.3/cpp/Stringification.html
```c
#include <stdio.h>

#define AFTER(x) X_##x

int main()
{
    char X_str[] = "test";
    printf("%s\n", AFTER(str));
    return 0;
}
```