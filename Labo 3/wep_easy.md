# WEP easy

WEP = Wired Equivalent Privacy

You can open an `ivs`-file with `aircrack-ng` in Kali Linux with the command: `aircrack-ng wep-easy-01.ivs`

## What is the BSSID and ESSID of the wireless network

BSSID: 00:0F:3D:A7:87:8C

ESSID: HOGENT_INT

## Who is the manufacturer of the Wireless Access Point (WAP)?

You can determine the manufacturer of the WAP by looking up the OUI (Organizationally Unique Identifier).

I've found the manufacturer with the site `https://macvendors.com` and entered the MAC-address and it's D-Link Corporation.

## How many IVs does this file contain?

13064 IVs

## How many bits were used by WEP for the RC4 encryption?

The output of the `ivs`-file shows 5 lines, which means aircrack-ng tries to crack a key of 5 bytes. A bit is 8 bytes, so 5 x 8 = 40. The IV (Initialization Vector) is always one of 24 bits (3 bytes x 8).

So 40 + 24 = 64 bits.

## What command(s) did you use to find this information?

`aircrack-ng -n 64 wep-easy-01.ivs`

Now I can see the `KEY FOUND! [ 00:92:43:33:33 ]` which has 5 bytes (10 hex digits)
