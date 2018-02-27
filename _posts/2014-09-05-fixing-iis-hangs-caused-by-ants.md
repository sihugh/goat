---
layout: post
title: Fixing IIS hangs caused by Ants Performance Profiler
categories: iis
description: IIS hung after recycling app pools, requiring an iisreset to fix.
---

One of our test boxes was suffering from IIS hangs after an application pool recycle - generally after either deploying an WSP or modifying a web.config.
The hang was accompanied by an error message in the Application event log: "Failed to CoCreate profiler".

The server had Ants Performance Profiler on it and I'd noticed the same error on my Dev box after using the same software, so suspected a culprit.

The Redgate articles I found suggested initially checking the permissions on the installation directories to ensure that the app pool accounts have read permissions.  This did not help our problem.

The second one suggested deleting the Environment value under the HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W3SVC key.  (This contradicts the MSDN article below, but after backing up the key I tried it anyway.)

I expect that in some circumstances this Environment value can contain more items than just those of a troublesome app, so should be done with care.  Anyway, it fixed our issue, so all's good!


[http://blogs.msdn.com/b/dougste/archive/2009/12/30/failed-to-cocreate-profiler.aspx](http://blogs.msdn.com/b/dougste/archive/2009/12/30/failed-to-cocreate-profiler.aspx "Failed to CoCreate Profiler - MSDN")

[http://documentation.red-gate.com/display/APP8/IIS+stops+working+after+profiling+web+applications](http://documentation.red-gate.com/display/APP8/IIS+stops+working+after+profiling+web+applications "IIS stops working after profiling web applications - redgate")
