---
layout: post
title:  "Remove the annoying apploc.tmp"
date:   2009-02-15
tags: C#
---
I used MS AppLocale to play some game in other languages. After running it, there will be an apploc.tmp file, which causes MS installer to generate unrecognizable characters in future installation. To my supprise, MS AppLocale does not provide a mechanism to remove that file, and I decide to devise my own program to remove it.

The native C++ approach is not popular any more. I tried some times, and found the service may not be stopped correctly. The main point is, you have to derive your own class from
```cpp
CAtlServiceModuleT< CMyCleanerModule, IDS_SERVICENAME >
```
and use RTTI in the Run method in the derived class. MS invented a new keyword: __super, which provides a very similar mechanism like the super keyword in Java, and base keyword in C#. So you don’t have to write
```cpp
CAtlServiceModuleT<CMyCleanerModule, IDS_SERVICENAME>* pasm = dynamic_cast<CAtlServiceModuleT<CMyCleanerModule, IDS_SERVICENAME>*>(this);
```
MS provide a good and complete tutorial for .net Windows services. The coding is straightforward, but you can not use the timer control in System.Timer, nor the timer in System.Windows.Forms, because of this bug: http://support.microsoft.com/default.aspx?scid=kb;en-us;842793. And I have to use delegate instead of threading for simplicity, although the latter is not that difficult.

Finally, my code goes like this
```csharp
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Diagnostics;
using System.Linq;
using System.ServiceProcess;
using System.Text;
using System.IO;
using System.Threading;

namespace MyDotNetCleaner
{
    public partial class MyDotNetCleaner : ServiceBase
    {
        private Timer tm;
        public MyDotNetCleaner()
        {
            InitializeComponent();
            if (!System.Diagnostics.EventLog.SourceExists("MySource"))
            {
                System.Diagnostics.EventLog.CreateEventSource("MySource", "MyNewLog");
            }
            eventLog1.Source = "MySource";
            eventLog1.Log = "MyNewLog";

        }

        protected override void OnStart(string[] args)
        {
            TimerCallback timerDelegate = new TimerCallback(rmTmp);
            tm = new Timer(timerDelegate, null, 1000, 1000);
        }

        protected override void OnStop()
        {
        }

        private void rmTmp(object state)
        {
            if (File.Exists("C:\\WINDOWS\\AppPatch\\AppLoc.tmp"))
            {
                File.Delete("C:\\WINDOWS\\AppPatch\\AppLoc.tmp");
                eventLog1.WriteEntry("AppLoc.tmp deleted");
            }
        }
    }
}
```
Very simple, but it works :D
