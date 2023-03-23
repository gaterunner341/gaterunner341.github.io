---
layout: post
title: Companies Beware of Proprietary Data Uploaded to Virus Total
author: Phillip Kittelson
categories: cybersecurity
tags: [ cybersecurity, data labeling, data classification, Virus Total, proprietary  ]
date: 2023-03-23 12:00 -0500
image: confidential.jpg
alt: Confidential
---
[Virus Total](https://www.virustotal.com) is an amazing tool, used by cybersecurity professionals across the world, and across the many industries in the government and private sectors. But beware, just like the saying anything posted on the Internet will be there forever. Analyst might routinely upload documents to Virus Total to detect known malicious code.

![VTImage](./assets/images/VTResults.png)

The average user who browses and searches Virus Total may only see indicators such as IP addresses, hashes, and file names, however, anyone with an enterprise account can download the uploaded content.

Virus Total supports search modifiers which allow tailoring search results to including file type and file name or labels, and more here on [VT's support poral](https://support.virustotal.com/hc/en-us/articles/360001385897-File-search-modifiers){: .hover-underline-animation target="_blank"}.

A savvy searcher with an enterprise account could locate PDF, Word Document, Excel, and other file types which could include words such as _restricted_, _proprietary_, _confidential_, _Confidential PII_, _Attorney-Client Privileged_, _Restricted_, and just about any label a company may use to label its confidential data, in its file name. Further narrowing searches down could narrow result in finding data from specific organizations, or industries. Simple Google searches can reveal how a company labels its internal confidential data via their guides. [Here is an example](https://www.premera.com/documents/030658.pdf){: .hover-underline-animation target="_blank"}.

Security analyst should be cautious when uploading files to any third party, regardless of the intent or purpose.