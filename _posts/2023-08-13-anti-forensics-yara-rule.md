---
layout: post
title: Anti-forensics YARA rules
author: Phillip Kittelson
categories: cybersecurity
tags: [ cybersecurity ]
date: 2023-08-12 09:00 -0500
image: yara.jpg
alt: Anti-forensics YARA rules
---
Recently, **[Xavier Mertens](https://isc.sans.edu/handler_list.html#xavier-mertens}**, of the **[SANS Internet Storm Center](https://isc.sans.edu/}** Mertens, **[posted](https://isc.sans.edu/diary/Show+me+All+Your+Windows/30116/){: .hover-underline-animation}** about a python script he found which uses the Windows API with a call to GetWindowText(). With my education in digital forensics, I find anti-forensics methods interesting. Anti-forensics includes methods designed to prevent, slow down, or impede static of dynamic analysis.

The code of interest is shown below. The defined `check_windows()` method further defines `winEnumHandler`, with calls to `GetWindowTextA()`, and checks for a list of stings from an array. These strings are common debugging or forensics tools which could are often installed in a forensics virtual machine or sandbox. After checking for the tools, the code attempts to determine the `ProcessID` of the window, and terminate it with `TerminateProcess()`:

```
def check_windows():
    @ctypes.WINFUNCTYPE(ctypes.c_bool, ctypes.POINTER(ctypes.c_void_p), ctypes.POINTER(ctypes.c_void_p))
    def winEnumHandler(hwnd, ctx):
        title = ctypes.create_string_buffer(1024)
        ctypes.windll.user32.GetWindowTextA(hwnd, title, 1024)
        if title.value.decode('Windows-1252').lower() in {'proxifier', 'graywolf', 'extremedumper', 'zed', 'exeinfope', 'dnspy', 'titanHide', 'ilspy', 'titanhide', 'x32dbg', 'codecracker', 'simpleassembly', 'process hacker 2', 'pc-ret', 'http debugger', 'Centos', 'process monitor', 'debug', 'ILSpy', 'reverse', 'simpleassemblyexplorer', 'process', 'de4dotmodded', 'dojandqwklndoqwd-x86', 'sharpod', 'folderchangesview', 'fiddler', 'die', 'pizza', 'crack', 'strongod', 'ida -', 'brute', 'dump', 'StringDecryptor', 'wireshark', 'debugger', 'httpdebugger', 'gdb', 'kdb', 'x64_dbg', 'windbg', 'x64netdumper', 'petools', 'scyllahide', 'megadumper', 'reversal', 'ksdumper v1.1 - by equifox', 'dbgclr', 'HxD', 'monitor', 'peek', 'ollydbg', 'ksdumper', 'http', 'wpe pro', 'dbg', 'httpanalyzer', 'httpdebug', 'PhantOm', 'kgdb', 'james', 'x32_dbg', 'proxy', 'phantom', 'mdbg', 'WPE PRO', 'system explorer', 'de4dot', 'x64dbg', 'X64NetDumper', 'protection_id', 'charles', 'systemexplorer', 'pepper', 'hxd', 'procmon64', 'MegaDumper', 'ghidra', 'xd', '0harmony', 'dojandqwklndoqwd', 'hacker', 'process hacker', 'SAE', 'mdb', 'checker', 'harmony', 'Protection_ID', 'PETools', 'scyllaHide', 'x96dbg', 'systemexplorerservice', 'folder', 'mitmproxy', 'dbx', 'sniffer', 'http toolkit'}:
            pid = ctypes.c_ulong(0)
            ctypes.windll.user32.GetWindowThreadProcessId(hwnd, ctypes.byref(pid))
            if pid.value != 0:
                try:
                    handle = ctypes.windll.kernel32.OpenProcess(1, False, pid)
                    ctypes.windll.kernel32.TerminateProcess(handle, -1)
                    ctypes.windll.kernel32.CloseHandle(handle)
                except:
                    pass
            exit_program(f'Debugger Open, Type: {title.value.decode("utf-8")}')
        return True

    while True:
        ctypes.windll.user32.EnumWindows(winEnumHandler, None)
        time.sleep(0.5)
```
The sample Xavier found is available on VirusTotal, and is detectable using a YARA rule from InQuest labs which centers around the Windows API function call. This alert is pretty high-level, and will result in a lot of false positives. I have never created YARA rules before, so with the combination of an interesting topic to me, and the prospect of learning something new, I decided to try and craft a YARA rule which would focus on code which either enumerates a window’s title text or terminates a process and while looking for for the list of tools shown in the original malicious Python code.

My final YARA rule can be found here in my **[GitHub repo](https://github.com/gaterunner341/YaraRules/tree/main/Anti_Forensics_Window_Enumeration){: .hover-underline-animation}**.

After setting up my YARA rule title, I define the variables to search for. In the case of both the `GetWindowTextA` and the `TerminateProcess()` calls, I use both strings, ignoring upper or lower case, and include the wide option, then include a hexadecimal value of each string.

```
$GetWindowText1="GetWindowTextA" nocase wide
$GetWindowText2={47 65 74 57 69 6E 64 6F 77 54 65 78 74 41}

$TermProcess1="TerminateProcess" nocase wide
$TermProcess2={54 65 72 6D 69 6E 61 74 65 50 72 6F 63 65 73 73}
```

After this, I include a lengthy list of the tools from the malicious script, also ingnoring case, and opening up with the wide option:
```
$WindowTitle1="proxifier" nocase wide
$WindowTitle2="graywolf" nocase wide
$WindowTitle3="extremedumper" nocase wide
$WindowTitle4="zed" nocase wide
$WindowTitle5="exeinfope" nocase wide
[continued]
```

For my conditions, I want to find binaries which are referencing my tool list, and either 1) trying to enumerate the window title, or 2) attempting to terminate a process:
```
($GetWindowText1 or $GetWindowText2) or ($TermProcess1 or $TermProcess2) and any of ($WindowTitle*)
```

Other YARA rules I come up with will be available on both my projects page, and this **[GitHub repo](https://github.com/gaterunner341/YaraRules/tree/main){: .hover-underline-animation}**.