# Capture your own DHCP traffic

## Capture instructions

Make sure that the Kali Linux is connected using the (default) VirtualBox NAT mode.

Release the IP-address of your network card: `sudo dhclient -r`

This command didn't show anything, but when I used the Verbose mode `-v`, it worked! I've got this output on the command line.

```console
┌──(osboxes㉿osboxes)-[~]
└─$ sudo dhclient -r -v
Internet Systems Consortium DHCP Client 4.4.3-P1
Copyright 2004-2022 Internet Systems Consortium.
All rights reserved.
For info, please visit https://www.isc.org/software/dhcp/

Listening on LPF/eth0/08:00:27:bb:74:59
Sending on   LPF/eth0/08:00:27:bb:74:59
Sending on   Socket/fallback
```

Let the DHCP client process negotiate a new IP address: `sudo dhclient`.

I've got this output:

```console
──(osboxes㉿osboxes)-[~]
└─$ sudo dhclient
Error: ipv4: Address already assigned.
```

In WireShark I can see an extra capture for `DHCP`.

Stop the capture and save the results as a `.pcap`-file.

## Questions related to your capture


