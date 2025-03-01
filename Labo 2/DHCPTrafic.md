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

1; Are DHCP messages sent over UDP or TCP?

UDP = User Datagram Protocol (It is a communication protocol used across the internet for time-sensitive transmissions)

DHCP Discover = client requesting an IP address.

DHCP Offer = server responding with an IP.

2; What is de IP-address of your DHCP-server?

DHCP Offer = server responds with an IP address and the server's IP is shown as `Server Identifier`. The DHCP Server Identifier is `10.0.2.2`.

3; Draw a timing diagram illustrating the sequence of the first four-packet Discover/Offer/Request/ACK DHCP exchange between the client and server. For each packet, indicated the source and destination port numbers.

DHCP Discover - from client to server, source port: 68, destination port: 67

DHCP Offer - from server to client, source port: 67, destination port: 68

DHCP Request - from client to server, source port: 68, destination port: 67

DHCP ACK - from server to client, source port: 67, destination port: 68

4; A host uses DHCP to obtain an IP address, among other things. But a host's IP address is not confirmed until the end of the four-message exchange! If the IP address is not set until the end of the four-message exchange, then what values are used in the IP datagrams in the four-message exchange? For each of the four DHCP messages (Discover/Offer/Request/ACK DHCP), indicate the source and destination IP addresses that are carried in the encapsulating IP datagram.

DHCP Discover - source IP: 0.0.0.0 (client does not have an IP yet), destination IP: 255.255.255.255 (broadcast)

DHCP Offer - source IP: 10.0.2.2 (server's IP address), destination IP: 255.255.255.255 (broadcast)

DHCP Request - source IP: 0.0.0.0 (client still does not have an IP), 255.255.255.255 (broadcast)

DHCP Ack - source IP: 10.0.2.2 (server's IP address), destination IP: 255.255.255.255 (broadcast)

The key insight is that the client uses the special address 0.0.0.0 as the source for its messages since it doesn't have a confirmed IP yet, and broadcasts (255.255.255.255) are used as the destination to ensure the messages reach their intended recipients despite not having specific addresses configured.

The DHCP server always uses its own IP address as the source for the messages it sends. Only after receiving the final DHCP ACK does the client configure its interface with the assigned IP address.

5; Explain the purpose of the lease time. How long is the lease time in your experiment?

Lease time is the amount of time in minutes or seconds a network device can use an IP Address in a network. The IP Address is reserved for that device until the reservation expires.

In WireShark you can find the lease time in the DHCP ACK at Option (51) IP Address Lease Time. The length is for and the lease time is 1 day (86400).
