---
layout: post
title: A Simple Query to hunt for CVE-2023-38831 WinRAR Exploitation
author: Phillip Kittelson
categories: cybersecurity
tags: [ cybersecurity ]
date: 2023-08-31 06:00 -0500
image: winrar.webp
alt: A Simple Query to hunt for CVE-2023-38831 WinRAR Exploitation
---
The great thing about threat queries are: they don’t have to be overly complicated. Start out simple, and expand the query to include, exclude, or generate the desired output.

I wrote a **very simple** query to find exploitation of WinRAR  under CVE-2023-38831. This exploitation is rather simple as well, with a specially crafted RAR archive with just three files. Many resources already outline the technical details of the file, one of those **[here](https://www.group-ib.com/blog/cve-2023-38831-winrar-zero-day/){: .hover-underline-animation target="_blank"}**, so I will not delve deeper into the minutia of it. Rather, let’s talk about my method for making the query.

My finished query is:

```
event_simpleName=ProcessRollup2 (ParentBaseFileName=winrar.exe FileName=cmd.exe)
| stats count by ParentBaseFileName FileName CommandLine
```

After a colleague of mine discovered a **[proof of concept](https://github.com/BoredHackerBlog/winrar_CVE-2023-38831_lazy_poc){: .hover-underline-animation target="_blank"}** (POC) for the CVE, I wanted to find out a way to detect the execution. I had to find a vulnerable version of WinRAR, and the official WinRAR site, of course, removed previously vulnerable versions. So, I turned to the WayBack Machine, and browsed for a previously published day I could find links to the older versions, and counted on the link still working. I was correct, and settled on version 6.11.

![FinalResult](./assets/images/blog_photos/20230831-WinRAR/wayback.png){: width="900px";height="auto"}

After installing WinRAR 6.11 in a sandbox, I modified the RAR archive I found in the POC to simply open MSPaint with **`start mspaint`** command in a **`.cmd`** file, and executed the payload.

The POC also states **`.bat`** files work as well, so I changed the file extension and re-detonated.
After that, I turned to my trusty EDR/SEIM tool, and plugged in a simple search: `winrar.exe`.

This of course, found the installation of WinRAR, my detonations above, and other event noise logged with 25 events. Twentyfive may not be a big issue, but in an enterprise environment, you’ll have thousands of results from this query. I wanted to only see the results of just the exploitation, so I modified my query to show new processes running:

**`event_simpleName=ProcessRollup2 winrar.exe`**

This reduced my events to seven, but still not good enough to roll enterprise. I wanteded to exclude items that were not from WinRAR as the parent process, so I went with:

**`event_simpleName=ProcessRollup2 winrar.exe ParentBaseFileName=winrar.exe`**

Down to four events, but I wanted to narrow my list even further, and only see those which resulted in commands run and which spawned from WinRAR:

**`event_simpleName=ProcessRollup2 (ParentBaseFileName=winrar.exe FileName=cmd.exe)`**

This gave me my two events, the **`.cmd`** and the **`.bat`** executions. Now I wanted to see those in an easier format to sift through for hunting in an enterprise environment, so I added my stats count:

**` | stats count by ParentBaseFileName FileName CommandLine`**


![FinalResult](./assets/images/blog_photos/20230831-WinRAR/WinRARCVE.png){: width="900px";height="auto"}