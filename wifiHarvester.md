---
layout: default
---

## WiFi Harvester

[WiFi Harvester](https://github.com/gaterunner341/wifiHarvester){: .hover-underline-animation target="_blank"} is a Python script which gathers information about the saved Wi-Fi profiles on
the system the program is executed on.

Available in this repository is the .py source code file and an executable file which can be run on a system without Python installed.  Both the executable and the .py file can be run from a USB drive, and will save the exported information to a text file located in the same folder using the host name of the system.

The program collects the following information:

-	Wi-Fi Network SSID
-	Network Password, if saved in the profile
-	MAC Randomization Indicator
-	Connection Mode Indicator
-	SSID Count

The Wi-Fi SSID is important to identify the network in question.  Additionally, if the password for the connection is saved in the system’s profiles, this will also be collected.  MAC Randomization enables an examiner to determine if the connection potentially had difference MAC addresses when the system was connected.  The connection mode indicates if the connection could be accomplished automatically, or if a user needed to make the connection manually.  SSID Count indicates if that network connection had more than one SSID associated with that connection.

<i class="fa-solid fa-backward" style="padding-right: 0.3em;margin-left: -0.9em;color: #8B0000;"></i>[Back...](./projects.html){: .hover-underline-animation}
