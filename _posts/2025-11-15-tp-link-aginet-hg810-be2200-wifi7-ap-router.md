---
layout: post
title:  "TP-Link Aginet HB810 BE22000 Tri-Band Mesh Wi-Fi 7 Router"
published: true
date:   2025-11-15
tags:   hardware networking router
comments: true
---

<img src="https://i.ebayimg.com/images/g/HwUAAeSwiqJoqQ3w/s-l1200.jpg" style=" width: 100%; height: 400px; object-fit: cover; object-position: 50% 60%;">

Just over a year ago, [2degrees][1] announced that they will be distributing the [TP Link BE22000 (HB810)][2] router for their [HyperFibre][3] customers.

Today I picked up this unit, *out of box*, without the proper adapter (12V 5A) - I was provided a random one at 2A. But with the cost of this router, it's okay. I've got a power adapter on the way from [AliExpress][7]. This retail version of the HB810 retails at [PBTech][6] at NZD$1,015.28 incl GST - but $947 on discount/promo and is currently available from [HarveyNorman][6.1] at NZD$1,036. I picked this unit up off Facebook Marketplace, incredibly cheap - *lets just say that, although it wasn't free, but cheap. I'm not gonna ask questions and just accept it!* 🤣

So there is a retail box-store Deco and a [Aginet][8] edition of this router, the Aginet version of this router which appears to be more for ISPs to distribute to customers - nearly identical but with HomeShield Parental Controls and HomeShield Security have been removed, as described in [this article][4] from Juha Saarinen on [Interest][5].

I plan to make this my primary router, replacing my aging although reliable [Linksys WRT1900AC][9] with [OpenWRT][10] installed. *Which is a recommend firmware upgrade for **any** WRT1900AC Owner!!* 

Updates: below, January 2026.

## Overheating & Crashing Issues


I've been using this router for a bit now, on a 900/500Mbit 2degrees network fibre connection, well ventilated living room - but this thing crashes, needing to be unplugged for a couple of minutes, turned back on - not daily but every couple of days to a few days.

My internet connection should be no issue for this router, yes its an heavily active connection, not activity you'd find from a typical "home router" - but even though, it should still be able to handle it without issue.

I'm somewhat unsure of why it's crashing but the network just entire drops, everything. Just gone! But works the moment you reboot it, everything works as normal again.

**Solution:** [USB Powered Computer PC Case Fan 120mm 5V Silent Chassis Cooler](https://www.aliexpress.com/item/1005008486440775.html)

Since using this, the HB810 router has not crashed - at all and the general active temperature of the unit has dropped.

I suspect that the routers fan curves are held back too far, there are no adjustments for different fan speed modes or any kind of control in the firmware from Aginet.

It would be great if Aginet would release the firmware, or a firmware for advanced users, allowing for more granular control over the router itself - this is a real downside and a major limiting factor to this router.

This router would be a great option for [OpenWRT](https://openwrt.org/) or DD-WRT, *preferably for OpenWRT*.

## Port-Forwarding

Additionally the amount of Port-Forwarding is limited to 20 rules. **Why?!**

I am an advanced user, this is a great router - its an expensive router, but you're given it the firmware control of a $30 router 15years ago.

I have no idea why Aginet limited the port-forwarding. Limiting it doesn't seem like a feature limitation that would urge a user to purchase a [Deco version of the HB810][6].

## Undocumented Telnet Access

There is **no documentation** regarding this anywhere.

This console is extremely limited and appears to be just designed to allow for more a remote administration for wireless configuration, there are no other commands available that i can find other than `wlctl` which appears to be "Wireless Control". 


```plain
$ telnet
telnet> open 192.168.1.1
Trying 192.168.1.1...
Connected to 192.168.1.1.
Escape character is '^]'.

username:admin
password:admin
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Welcome To Use TP-Link COMMAND-LINE Interface Model.
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
TP-Link>help
normal mode commands:
        clear           ---     clear screen
        exit            ---     leave to the privious mode
        help            ---     help info
        history         ---     show histroy commands
        logout          ---     logout cli model
        wlctl           ---     wireless config

TP-Link>wlctl
wlctl set <2g|5g|6g|all> [ --ssid <ssid> [base64] ]
                         [ --bandWidth <Auto|20M|40M|80M|160M> ]
                         [ --switch <on|off> ]
                         [ --qss    <on|off> ]
                         [ --wepkey <key> [base64] [keyindex] ]
                         [ --pskkey <key> [base64] ]
                         [ --sec [none]
                                 [<wep> <auto|open|shared> <key> [base64] [keyindex]]
                                 [<psk> <auto|wpa|wpa2> <auto|tkip|aes> <key>] [base64] ]
                         [ --wds [ssid] [base64] ]
                         [ --disconnect-wds ]

wlctl show <2g|5g|6g>
cmd:SUCC
TP-Link>
```
Upon thinking about it, I suspect this is a obscured backdoor for IT support. Allowing a technician to connect via eithernet or a users computer via the wired/wireless network, login without needing their login details, update their WiFi, change configuration to the users liking.

There appears to be an active ssh daemon on the router, I have been unable to gain access to it as of yet.

```plain
$ ssh admin@192.168.1.1
admin@192.168.1.1's password: admin
Permission denied, please try again.
admin@192.168.1.1's password: passwd
Permission denied, please try again.
admin@192.168.1.1's password: [router web interface password]
admin@192.168.1.1: Permission denied (publickey,password).
```
I think this might be unlocked eventually, but the password is unknown - this thing should have a UART interface right?

If anyone gains access, please let me know!

# Web Interface Login Issue

If you experience a blank page issue, unable to login or it just refuses to let you in if you access `http://192.168.1.1/` you may need to use `http://tplinkwifi.net/`.



[1]: https://www.2degrees.nz/media-release/2degrees-launches-new-Wi-Fi-7-modem
[2]: https://www.tp-link.com/us/service-provider/home-wifi-system/hb810/
[3]: https://youtu.be/Wk0nIC80azI
[4]: https://www.interest.co.nz/technology/130181/2degrees-bundles-tp-link-deco-be85-wi-fi-7-system-hyperfibre-connections-its
[5]: https://www.interest.co.nz/
[6]: https://pbtech.co.nz/product/NETTPL7851/TP-Link-Deco-BE85-BE22000-Tri-Band-WiFi-7-Whole-Ho
[6.1]: https://www.harveynorman.co.nz/networking-smart-home-and-home-phones/networking/mesh-networking/tp-link-deco-be85-be22000-tri-band-mesh-wi-fi-7-system-1-pack-white.html
[7]: https://www.aliexpress.com/item/1005006689701639.html
[8]: https://www.tp-link.com/us/landing/aginet-solution/
[9]: https://downloads.linksys.com/downloads/datasheet/MR19065_NET_WRT_PB_14PB007_WRT1900AC-ME_UK.pdf
[10]: https://openwrt.org/toh/linksys/wrt1900ac





