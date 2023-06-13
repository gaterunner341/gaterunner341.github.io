---
layout: default
---

## <i class="fa-solid fa-bullseye" style="color:#191970" aria-hidden="true"></i> Hunt Queries

### __T1176: Browser Extensions__
__MITRE Description__: Adversaries may abuse Internet browser extensions to establish persistent access to victim systems. Browser extensions or plugins are small programs that can add functionality and customize aspects of Internet browsers. They can be installed directly or through a browser's app store and generally have access and permissions to everything that the browser can access

__Analysis__: Browser extensions are a huge pain for any organization. Users are constantly looking for solutions to make their work easier, faster, or more productive. Browser extensions are a great way to integrate different software and add more capabilities. However, browser extensions are also a threat vector, and is exploited by adversaries in the wild, including extensions not in a browser’s official webstore. Execution of non-webstore browsing extensions can also be launched through a short cut parameter. The below hunt query allows for the detection for and grouping and sorting of this type of behavior.

__CrowdStrike__:
```
event_platform=win CommandLine IN (*--load-extension) NOT ([known exclusion] OR [known exclusion}])
| eval CommandLine=lower(CommandLine)
| eval CommandLine=replace(CommandLine,program files\\\\google\\\\chrome\\\\application\\\\chrome.exe","CHROMEPATH)
| eval CommandLine=replace(CommandLine,program files \(x86\)\\\\google\\\\chrome\\\\application\\\\chrome.exe","CHROMEPATH)
| eval CommandLine=replace(CommandLine,"users\\\\[^\\\\}+,"users\\USERNAME")
| stats dc(ComputerName) count by CommandLine
| sort + count
```