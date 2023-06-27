---
layout: post
title: How are you Securing a Remote Workforce?
author: Phillip Kittelson
categories: cybersecurity
tags: [ cybersecurity, remote work, telework, risk management, Plex, LastPass ]
date: 2023-03-05 19:00 -0500
image: remote.jpg
alt: Remote Work
---
How secure is your remote work force? If the remote COVID pandemic has taught us anything, it should be about securing a remote work force. In the early days, businesses literally had a one-day turn around from all on-site operations, to just about a 100% remote work force. I worked for a l large defense contractor company at the time, and when I saw the flip switch, I was home before lunch time.

Businesses operations, and data, were being compromised at an alarming rate since they were not prepared to secure a remote work force either at scale, or at all. Employees were now behind untrusted networks, potentially using out-of-date hardware without any of the bells, whistles, and defenses your on-premises suite of security tools would provide. Some businesses have learned, while, sadly, some have not. LastPass, a popular password manager service recently reported a compromise of their network where an attacker captured employee login credentials. An investigation showed an employee was running a severely out of date version of the popular Plex Media Server on their home computer. And when I say severely out of date, I am talking a CVE with a date of 2020, with about 78 Plex updates from that CVE fix to today.

Other organizations have had the same issue, with some military agencies not allowing users to map printers or install print drivers after dozens of reports of users downloading malicious drivers from the web while teleworking.

So, what do you do as a business owner with a remote work force? Do you require a full hardware and software list from devices running on your employee’s home networks? Where is the line drawn? Let me give you my opinion on securing remote users.

## Dedicated Hardware
News reports of the LastPass breach do not provide many details of the hack, but from reading about the vulnerability, and the type of malware delivered (key logger), I am going to make an educated guess the LastPass employee was at least logging into, and potentially performing LastPass work, using their personal computer. Organizations should take steps to ensure critical business operations, and access to company resources, are only granted using authorized hardware. A company must make a risk-based decision if they are going to issue computers to their employees to perform authorized telework. Is the price, and maintenance, of the hardware, worth the cost to put an employees work behind some set of security tools? In the case of a password management company, where trust by your users in your company is the basis for your business, yes it would. Implement policies discouraging employees from conducting company business on home computers, require the use of company hardware or consider sandboxed virtual machine solutions for remote work.
## Disallow Untrusted Connections
Some companies, and government agencies, have policies in place which do not allow employees to use untrusted networks while traveling. A home network “should” be a more trusted network, but compared to your company’s internal systems, and considering breaches like this recent LastPass hack, organizations need to understand home networks are not really trusted networks. Unless you are a tech geek like me, the average user probably do not have a firewall, endpoint detection, DNS sink holing, or other defense-in-depth type security tools implemented on their home network. Companies should definitely not allow connections to untrusted networks, such as the Wi-Fi at airports, restaurants, and hotels be used to access company resources. A better option would be requiring employees to use MiFi or hotspot devices, such as more trusted company phone or device instead of Wi-Fi at these locations.
## Culture of Security
Just short of having employees send in a hardware or software list for their home network, organizations should invest in developing a culture of security. Where employees understand outdated software on their home devices not only puts their ability to remote work at risk, but also endangers their own data and privacy as well. The LastPass hack could have also allowed the attacker to capture credit and debit card data, passwords to email accounts, and even financial institutions. I would hope the local credit union the employee uses for direct deposit has multi factor authentication (MFA) installed.
## Implement MFA
Speaking of multi-factor authentication, it sounded like the LastPass employee had not implemented a MFA option, or at least an out-of-band MFA. If this was the case, the employee could have received one-time-temporary passcode (OTTP) messages and would have been alerted to irregular activity for their account. If a rotating password were implemented, on an out-of-band solution, a username and password would have been useless to the attacker.
Keep in mind MFA solutions are not full proof. MFA spamming can cause MFA fatigue, and there are documented attacks where users have allowed logins just to shut up their MFA alerts. A better solution would be a rotating MFA code on a separate device from where the user is attempting to gain access from. Hardware security tokens, or even software-based rotting codes in authentication apps could be a good solution.
## Implement Compensating Controls
During the pandemic remote work, military agencies also had a dramatic shift in remote work requirements. Users quickly found out they could not access encrypted emails through web-based email portals, especially with the depreciation of S/MIME. Agencies had to evaluate how they could allow users to get work done while accessing required data at the same time. Evaluating if the email environment met encryption requirements versus encryption at the message level had to be evaluated. At the same time, not allowing file downloads from web-based email portals could be implemented as a compensating control.

Regardless of what controls or policies you implement to secure a remote work force, the decision makers in your organization need a clear understanding of the risks associated with allowing remote work and make informed decisions.