---
layout: post
title: Threat Hunting Tool Highlight - IOC-Fanger
author: Phillip Kittelson
categories: cybersecurity
tags: [ cybersecurity ]
date: 2023-08-27 09:00 -0500
image: fang.jpg
alt: Threat Hunting Tool Highlight - IOC-Fanger
---
<iframe width="560" height="315" src="https://www.youtube.com/embed/mU47YHOj-kY?si=KglhFcFi05LKqqfe" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

One of my favorite CommandLine tools is **[IOC-Fanger](https://github.com/ioc-fang/ioc-fanger){: .hover-underline-animation target="_blank"}**. I work with potentially malicious links and IP addresses, often obtain Indicators of Compromise (IOCs) or have to generate a report for others to read, where I do not want users to click on the links, or automated tools to resolve the hostname or IP address.
IOC-Fanger is a Python library, and can be installed using pip **`pip install ioc-fanger`**.

Alternatively, the tool can be cloned:
``` 
git clone https://github.com/ioc-fang/ioc_fanger.git && cd ioc_fanger;
python setup.py install --user;
```

After installation, you’ll have access to IOC-Fanger via the command line using **`fang`** and **`defang`** or, since it’s a Python library, you can import using **`import ioc_fanger`** and calling **`ioc_fanger.defang()`** or **`ioc_fanger.fang()`** your IOCs, or variables containing the IOCs, inside the ().

The **[Quick Start Page](https://ioc-fanger.hightower.space/quick-start/#installation){: .hover-underline-animation target="_blank"}** shows the use below:

```
import ioc_fanger

ioc_fanger.defang("example.com http://bad.com/phishing.php")  # example[.]com hXXp://bad[.]com/phishing[.]php
ioc_fanger.fang("example[.]com hXXp://bad[.]com/phishing[.]php")  # example.com http://bad.com/phishing.php
```
If you are using command line, you can **`echo`** an IOC and **`|`** the output to fang or defang, depending on which way you’re going.
```
echo www.malware.com | defang

output -> www[.]malware[.]com
```

```
echo www[.]malware[.]com | fang

output -> www.malware.com
```
Working with a large set of IOCs, can be stored in a txt file where you can **`cat`** the file contents out to the CommandLine and **`|`** into **`defang`** or **`fang`** and output that into anothet working text file.

```
cat ioc.txt | defang

output ->   www[.]malware[.]com
            1[.]1[.]1[.]1
            hXXps://malware[.]com
            hXXp://virus[.]ru
            172[.]16[.]66[.]33
```

IOC-Fanger works well with IOCs containing:
- https://
- http://
- Muliple periods, such as IP addresses