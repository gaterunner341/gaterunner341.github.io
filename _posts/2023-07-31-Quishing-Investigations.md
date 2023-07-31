---
layout: post
title: Quishing Investigations
author: Phillip Kittelson
categories: cybersecurity, threat hunting, phishing, quishing, cyberchef
tags: [ cybersecurity ]
date: 2023-07-31 12:00 -0500
image: chef.jpg
alt: Quishing Investigations
---
Quishing, or phishing involving QR codes has been on the rise. My opinion is: adversaries will take advantage of just about anything they can. Since COVID, a lot more people know what a QR code is and how to use them, just enough knowledge to be dangerous. I would wager you’ve probably walked into a restaurant sometime in the last three years and used your phone to scan a QR code to see the menu, or even place your order online. So have a lot of your users, especially the click happy ones, who will become QR scanning happy.

A task which should be familiar in cybersecurity is phising email analysis. Normally, these emails contain either a link, or attachment with a link, you can run through your favorite open-source intelligence tools, or try and download the malicious code to analyze in a sandbox environment. However, you may be confused when you receive a QR code-based quishing email. After all, it’s not just a simple link you can copy and paste. There are a few tools and methods you can use to help you get over the initial difference of how the URL is delivered to the user.

### [CyberChef](https://gchq.github.io/CyberChef/){: .hover-underline-animation target=”_blank”}
While you can Google QR code reader, or QR code decoder, and find any dozens of sites (maybe reputable, maybe not), one you should be using more is CyberChef.

CyberChef is a tool developed by the GCHQ, the UK’s intelligence, security, and cyber agency. The tool is hosted on Github and allows you to download a stand-alone version of the site for use on non-internet connected analyst environments. CyberChef allows you to use, and chain together, different data operations, which includes an operation to parse QR codes.

Most quishing emails will have an attached or embedded image file, which can be saved locally. Once saved, you should confirm the file itself does not contain any malicious code. After that, use the Parse QR Code operation, and click either use the option to Open file as input, or simply click and drag the image file into the empty input panel. You do not need to crop the image, CyberChef can handled the entire image, and will ignore anything no a QR code for this operation.

You should see the decoded URL in the Output panel. CyberChef does not make this link clickable, but if you need to send this URL to someone else, or include in a report, you’ll want to “defang” the URL so no one can accidentally click on the link and visit the malicious site. Luckily, CyberChef has anther URL operation called Defang URL. You can add the operation below the Parse QR Code operation. Now you have a defanged URL to send out.

### Scripting
If CyberChef isn’t too technical for you, or you don’t have authorization to download CyberChef to your analyst environment as a stand-alone, scripting languages could be a possibility for you.
A colleague of mine jammed out a Python script to decode a QR code image.

This script imports QRTools l library to perform the decode, and includes a replace method to defang the URL.
```
import qrtools
import sys

def decode(filename):
    qr=qrtools.QR()
    qr.decode(filename)
    print(qr.data.replace('http', 'hxxp').replace('.', '[.]'))

if __name__ == '__main__':
    file_name = sys.argv[1]
    decode(file_name)
```

I’m a major fan of mixing BASH and Python together, which gives you more options to run outputs through different tools. In my example below, I’m using BASH to store the Python script output into a variable and pipe it into a tool called **[IOC-Fanger](https://ioc-fang.github.io/){: .hover-underline-animation target=”_blank”}** using the defang option. I have the scripts available on my **[GitHub](https://github.com/gaterunner341/QRDecode/tree/main){: .hover-underline-animation target=”_blank”}**.

Here is the command syntax:
```
bash python3 QRDecode.sh [filename.png]
```

#### BASH Script:
```
#!/bin/bash
# Decode QR Code
decoded_data=$(python3 QRDecode.py $1)
# Pass decoded data to defang
echo "$decoded_data" | defang
```

#### Python Script:
```
import qrtools
import sys

def decode(filename):
    qr=qrtools.QR()
    qr.decode(filename)
    print(qr.data)

if __name__ == '__main__':
    file_name = sys.argv[1]
    decode(file_name)
```

Check out my list of useful **[CyberChef Recipies](https://www.phillipkittelson.com/CyberChef.html){: .hover-underline-animation target=”_blank”}**