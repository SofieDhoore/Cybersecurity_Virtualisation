# Network sniffing

## Example: 0-FTP.pcap

Capture van FTP activity

**How many TCP-connections are there?**

Statistics menu -> Conversations -> TCP Tab tells how many TCP connections there are. In this file: 45

**How is each TCP-connection starting?**

Every TCP-connection starts with a 3-way-handshake. This process ensures that both parties are ready for communication and that the connection is established reliably.

SYN (Synchronize): The initiating host (client) sends a packet with the SYN flag to the server to request a connection.

SYN-ACK (Synchronize-Acknowledge): The server responds with a packet that has both the SYN and ACK flags enabled.

ACK (Acknowledge): The client acknowledges receipt with an ACK packet. The connection is now established.

**Can you deduce the reason for the three data connections from the control connection?**

If you see three separate SYN, SYN-ACK, ACK handshakes on different ports, you know that three data connections have been used.

Request: PORT 157, 193, 214, 191, 19, 137. This means 157.193.214.191 as the IP-address. (19\*256) + 137 = 5001. 5001 is the port. If you put `tcp.port == 5001`, then you get all packets sent through this port.

SYN → Client requests a connection on port 5001.

SYN-ACK → Server confirms.

ACK → Client completes handshake.

You will see multiple PORT commands, each with a different port. If you enter this into Wireshark `tcp.flags.syn == 1`, you will see three separate SYN handshakes with different ports, this means three data connections are set up.

### For your information

FTP = File Transfer Protocol to transfer files between client and server.

TCP = Transmission Control Protocol to exchange data between networks.

## Exploring a first trace file

**Think of how DNS is working, on what ICMP is all about. The protocol is on the Network Layer and it used for error handling. Try to analyse which command has lead to this stream of packets. Be as precise as you can be.**

When you click on the lines, you can see type 8 and type 0, type 8 is a request, type 0 is a reply. It means it's a ping, it's using ping. There's an equal interval time between packets and one source and one destination IP.

ICMP = Internet Control Message Protocol

DNS = Domain Name System

## Analysing a HTTP capture

### lab1 Wireshark intro 2 HTTP basic.pcap

Indicate where in the message you've found the information that answers the following questions.

**Is the browser running HTTP version 1.0 or 1.1? What version of HTTP is the server running?**

The browser is running version 1.1. The request version is also 1.1

**What languages (if any) does your browser indicate that it can accept to the server?**

Accept-language = en, nl

**What is the IP address of your computer? Of the gaia.cs.umass.edu server?**

host: 157.193.215.200

gaia.cs.umass.edu: 128.119.245.12

**What is the status code returned from the server to your browser?**

Status code: 200 OK
