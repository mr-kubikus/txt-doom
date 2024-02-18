# Running DOOM on fischertechnik TXT controller
Brief instructions how to run opensource DOOM port[1] on the TXT controller from Fischertechnik GmbH


## System requirements
Target:
- Fischertechnik TXT controller with firmware 4.7.0


## Start from release binaries right now
1. Download txt-doom.tar.gz file from github releases - https://github.com/mr-kubikus/txt-doom/releases
2. Connect your PC to the target via WIFI or USB link. Use following IP addresses to reach the TXT:
    USB       - 192.168.7.2
    WIFI      - 192.168.8.2
    Bluetooth - 192.168.8.2
3. Default password is ROBOPro
4. Upload txt-doom.tar.gz to the target:
~~~
scp txt-doom.tar.gz ROBOPro@192.168.7.2:/tmp
~~~
5. Connect to the target via ssh. Unpack first and than start the game:
~~~
ssh ROBOPro@192.168.7.2
cd /tmp
tar xzf txt-doom.tar.gz
cd txt-doom
./prboom-plus -width 240 -height 240 -warp 1
~~~
6. Optionally you may kill the TxtControlMain to prevent access to the shared LCD


## Dependencies
External:
- prboom-plus_2.5.1.4 - https://github.com/coelckers/prboom-plus/tree/prboom-plus_2.5.1.4
- SDL-1.2.15 - http://www.libsdl.org/release/SDL-1.2.15.tar.gz

Provided with TXT firmware:
- ftrobopy + patch
- evemu


## Build
Build host:
- x86_64
- Windows 10
- VM Ubuntu 18.04

TODO: Prepare dockerfile for build


## Where to get a WAD file?
To start prboom-plus you need two wad[2] files:
* prboom-plus.wad - Patch WAD
* doom1.wad - Internal WAD

To get the prboom-plus.wad you should first build it from the prboom2/data folder 
using the toolchain for host architecture.

The shareware doom1.wad is available from [3]


## Input events
~~~
E: 5.546016 0004 0004 458756    # EV_MSC / MSC_SCAN             458756
E: 5.546016 0001 001e 0001      # EV_KEY / KEY_A                1
E: 5.546016 0000 0000 0000      # ------------ SYN_REPORT (0) ---------- +5402ms
E: 5.674964 0004 0004 458756    # EV_MSC / MSC_SCAN             458756
E: 5.674964 0001 001e 0000      # EV_KEY / KEY_A                0
E: 5.674964 0000 0000 0000      # ------------ SYN_REPORT (0) ---------- +128ms
~~~


## References
1. https://github.com/coelckers/prboom-plus/tree/prboom-plus_2.5.1.4
2. https://doomwiki.org/wiki/WAD
3. https://doomwiki.org/wiki/DOOM1.WAD