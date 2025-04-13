# WPA medium

WPA = WiFi Protected Access

You can open a `cap`-file with `aircrack-ng` in Kali Linux with the command: `aircrack-ng wpa-medium-01.cap`.

## What is the BSSID and ESSID of the wireless network?

BSSID: 00:0F:3D:A7:87:8C

ESSID: HOGENT_WPA_SEC

## How many 4-way handshakes does this capture file contain?

There's only 1 handshake:

![handshake](/images/handshake.png)

## What is the WPA password (as string)?

The password in this case is: `KEY FOUND! [ cbeeadcf ]`

## What command did you use to find this information?

`aircrack-ng -w shortwordlist.txt wpa-easy-01.cap`

## Which wordlist did you use?

First I used the command: `sudo locale-gen en_US.UTF-8`, to configure locale UTF-8.

I've made a new wordlist with crunch: `crunch 6 8 abcdef shortwordlist.txt`
