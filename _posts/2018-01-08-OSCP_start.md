---
layout: post
title: OSCP Start pt. 1
---

Like I mentioned in previous post I moved start of my PWK course to 17.12.2017. I recived all materials on time, however probably becouse of holydays athmosphere I wasn't fealing like learning new stuff so I just spent time with family setting my new Year goals and plying some games. One thing I did was to prepare Kali VM, all aliases, and I also tested connection to OSCP network.

Today after Xmas and New Year reset from any security related things I started reading and doing first excercises from PWK Course, so far easy peasy but I think things start to be much harder ;)

I didn't mention that before Xmas I created and finished my VHL report after rooting 20+ boxes. After that I recived certifcate of completion which is very nice. I also wrote a review on their page, you can read it [here](https://www.virtualhackinglabs.com/reviews/)

Some tips:
I created script that you can then alias, so every time you want to connect to OSCP network run this script:  
Alias script (put it to .bashrc):  
```
alias oscpvpn='/root/Desktop/connect/conn.exp OS-XXXX password &'  
```
Script:

```
#!/usr/bin/expect -f

set config "/root/Desktop/connect/OS-33596-PWK.ovpn"
set username [lrange $argv 0 0]
set password [lrange $argv 1 1]

set force_conservative 1  ;# set to 1 to force conservative mode even if
                          ;# script wasn't run conservatively originally
if {$force_conservative} {
        set send_slow {1 .1}
        proc send {ignore arg} {
                sleep .1
                exp_send -s -- $arg
        }
}

set timeout -1
spawn openvpn --script-security 2  --config $config --auth-user-pass
match_max 100000
expect -exact "Enter Auth Username: "
send -- "$username\r"
send -- "$password\r"

interact
```

--
OSCP status:  
Current number of excercises done: 1  
Current number of rooted boxes: 0  

Happy new Year and tons of shells poped :) !!
