---
layout: post
title:  "Cheap memory detector for Visual Studio IDE"
date:   2007-01-02
tags: C++
---
memleak.h
```cpp
#ifndef MEMLEAK_H
#define MEMLEAK_H

#pragma once
#define _CRTDBG_MAP_ALLOC
// use this file in VS IDE only!!!!!
// ref: ms-help://MS.MSDNQTR.v80.en/MS.MSDN.v80/MS.VisualStudio.v80.en/dv_vsdebugnative/html/43eedaa1-3f26-463c-9c31-ae21f10ed16d.htm
#include <crtdbg.h>

class leak_reporter
{
private:
    static leak_reporter instance;
    leak_reporter()
    {
        _CrtDumpMemoryLeaks();       
        _CrtSetDbgFlag ( _CRTDBG_ALLOC_MEM_DF | _CRTDBG_LEAK_CHECK_DF );
        _CrtSetReportMode( _CRT_ERROR, _CRTDBG_MODE_DEBUG );
    }
};
leak_reporter leak_reporter::instance;

#endif
```
