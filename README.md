Introduction
============
This exploit was developed based on the technical description by ```depthsecurity```
```
https://depthsecurity.com/blog/cve-2017-6079-blind-command-injection-in-edgewater-edgemarc-devices
```

Description
============
The HTTP web-management application on Edgewater Networks Edgemarc appliances has a hidden page that allows for user-defined commands such as specific iptables routes, etc., to be set. You can use this page as a web shell essentially to execute commands, though you get no feedback client-side from the web application: if the command is valid, it executes. An example is the wget command. The page that allows this has been confirmed in firmware as old as 2006.

Device Detection
===============
Nmap will identify the device from its web server as shown
![Alt text](pics/nmap.png?raw=true "nmap")


Usage
======
```
 _____    _                          _
| ____|__| | __ _  _____      ____ _| |_ ___ _ __
|  _| / _` |/ _` |/ _ \ \ /\ / / _` | __/ _ \ '__|
| |__| (_| | (_| |  __/\ V  V / (_| | ||  __/ |
|_____\__,_|\__, |\___| \_/\_/ \__,_|\__\___|_|
            |___/
 _____    _
| ____|__| | __ _  ___ _ __ ___   __ _ _ __ ___
|  _| / _` |/ _` |/ _ \ '_ ` _ \ / _` | '__/ __|
| |__| (_| | (_| |  __/ | | | | | (_| | | | (__
|_____\__,_|\__, |\___|_| |_| |_|\__,_|_|  \___|
            |___/
 _____            _       _ _
| ____|_  ___ __ | | ___ (_) |_
|  _| \ \/ / '_ \| |/ _ \| | __|
| |___ >  <| |_) | | (_) | | |_
|_____/_/\_\ .__/|_|\___/|_|\__|
           |_|


                 Edgewater Edgemarc Exploit CVE-2017-6079
                 Coded By: Mostafa Soliman
                 
    [USAGE] CVE-2017-6079.py [operation] [TargetIP] [AttackerIP] [FilePath]
    operation: Either read / upload
    AttackerIP: IP address to receive the connection on
    TargetIP: IP address of the target running Edgewater Edgemarc server
    FilePath:  Remote file to download in case of "read" operation
               Local file to upload in case of "upload" operation
```

Exploit
========
The exploit assumes that the device has default root password which is ```default``` if this is not the case you will need to replace the ```Authorization```
The exploit has 2 modes of operation:
#### 1. Read
This mode allow the attacker to read any files on the vulnerable device.

![Alt text](pics/read-exploit.png?raw=true "read")


#### 2. upload
This mode allow the attacker to upload ELF file payload to ```/tmp/``` folder and execute it.
You will need to start listner to recieve the connection.

![Alt text](pics/upload-exploit.png?raw=true "upload")

