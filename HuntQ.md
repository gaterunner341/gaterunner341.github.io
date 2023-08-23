---
layout: default
---

## <i class="fa-solid fa-bullseye" style="color:#191970" aria-hidden="true"></i> Hunt Queries

### __T1176: Browser Extensions__ <i class="fa-brands fa-edge-legacy" style="color:#191970" aria-hidden="true"></i> <i class="fa-brands fa-chrome" style="color:#191970" aria-hidden="true"></i>
__MITRE Description__: Adversaries may abuse Internet browser extensions to establish persistent access to victim systems. Browser extensions or plugins are small programs that can add functionality and customize aspects of Internet browsers. They can be installed directly or through a browser's app store and generally have access and permissions to everything that the browser can access.

__Analysis__: Browser extensions are a huge pain for any organization. Users are constantly looking for solutions to make their work easier, faster, or more productive. Browser extensions are a great way to integrate different software and add more capabilities. However, browser extensions are also a threat vector, and are often exploited by adversaries in the wild, including extensions not in a browser’s official webstore. Execution of non-webstore browsing extensions can also be launched through a short cut parameter. The below hunt query allows for the detection for and grouping and sorting of this type of behavior.

![CSLogo](./assets/images/resume/cs.png){: style="width:20px;height:auto"} __Crowd Strike__ 
```
event_platform=win CommandLine IN (*--load-extension*) NOT (*[known exclusion]*)
| eval CommandLine=lower(CommandLine)
| eval CommandLine=replace(CommandLine,"program files\\\\google\\\\chrome\\\\application\\\\chrome.exe","CHROMEPATH")
| eval CommandLine=replace(CommandLine,"program files \(x86\)\\\\google\\\\chrome\\\\application\\\\chrome.exe","CHROMEPATH")
| eval CommandLine=replace(CommandLine,"program files\\\\microsoft\\\\edge\\\\application\\\\msedge.exe","EDGEPATH")
| eval CommandLine=replace(CommandLine,"program files \(x86\)\\\\microsoft\\\\edge\\\\application\\\\msedge.exe","EDGEPATH")
| eval CommandLine=replace(CommandLine,"users\\\\[^\\\\]+","users\\USERNAME")
| eval CommandLine=replace(CommandLine,"scoped\_dir[0-9]+\_[0-9]+","USERDATADIRECTORY")
| stats dc(ComputerName) count by CommandLine
| sort + count
```

![SplunkLogo](./assets/images/resume/splunk.webp){: style="width:20px;height:auto"} __Splunk__

```
sourcetype=WinEventLog EventCode=4688 Process_Command_Line IN (*--load extension)
| stats dc(ComputerName) by Process_Command_Line
```




### __Potential CAPTCHA Bypass__ <i class="fa-brands fa-edge-legacy" style="color:#191970" aria-hidden="true"></i> <i class="fa-brands fa-chrome" style="color:#191970" aria-hidden="true"></i>
__Analysis__: Web scrapers are always trolling the web, look for traffic specific to potential scrapers hitting CAPTCHA pages.

![SplunkLogo](./assets/images/resume/splunk.webp){: style="width:20px;height:auto"} __Splunk__
```
TERM(captcha) index=[proxy_index] url_domain=[domain_of_interest]
| bucket _time spam=10m
| stats count by _time c_ip action cs_method http_user_agent url
| where count > 5
| sort - count
```
