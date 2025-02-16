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

If we look at the echo (ping) request and reply messages, we can see that all packages have a TTL of 128. This can indicate that both machines run Windows. On Linux hosts, a TTL of 64 is typically used instead. So, if you would ping a linux machine from a windows host, you will see that the ping requests have a TTL of 128 and the ping replies will have a TTL of 64.

## Analysing a HTTP capture

### lab1 Wireshark intro 2 HTTP basic.pcap

Indicate where in the message you've found the information that answers the following questions.

**Is the browser running HTTP version 1.0 or 1.1? What version of HTTP is the server running?**

The browser (client) is running version 1.1. The request (server) version is also 1.1

**What languages (if any) does your browser indicate that it can accept to the server?**

Client accepts EN or NL as languages. Accept-language = en, nl

**What is the IP address of your computer? Of the gaia.cs.umass.edu server?**

Client (host): 157.193.215.200

gaia.cs.umass.edu: 128.119.245.12

**What is the status code returned from the server to your browser?**

Status code: 200 OK

This file illustrates the network traffic generated when a client (IP: 157.193.215.200) browses to a website (URL: <http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file1.html>).

First, the client needs to resolve the IP of the destination URL. The first 2 messages in the capture illustrate a DNS query sent to a DNS server (157.193.215.2) to get the A record for gaia.cs.umass.edu. The DNS server responds that the IP address is 128.119.245.12.

The next 3 messages are a TCP handshake between the client and the webserver gaia. Next, a GET request is sent from the client to the webserver to get the contents of /wireshark-labs/HTTP-wireshark-file1.html. In this message, we can see that the client browser uses HTTP/1.1. Furthermore, if we expand the HTTP part of this message, we can see that the browser accepts NL or EN as languages.

In the 8th message of the capture, we can see that the server responds to the HTTP request with status code 200 OK. All content (the HTML of the page) is included in this message, so the client can display the web page in the browser.

### lab1 Wireshark intro 3 HTTP with objects.pcap

**How many HTTP GET request messages did your browser send? To which Internet addresses (URLs) were these GET requests sent?**

4 GET requests

**Have a look at packet 20. Which HTTP return code did you receive? What does this indicate?**

Packet 20: HTTP 302 > URL redirection

**Can you tell whether your browser downloaded the two images serially, or whether they were downloaded from the two web sites in parallel? Explain.**

Images are sent in serial

This is a more complex example of network traffic generated when a client (IP: 157.193.215.200) browses to a website (<http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file4.html>). This time, not only the HTML page is downloaded, but also 2 images which are included in the HTML.

The capture starts with the client sending a DNS lookup for gaia.cs.umass.edu, and the DNS server (157.193.215.2) answers with IP 128.119.245.12.

The client then sends a HTTP GET request to gaia to retrieve the HTML page. In the HTML, two images are used, which need to be downloaded using separate GET requests.

The first image is downloaded from the same server (gaia). The second image however is located on a different server (manic.cs.umass.edu). Before we can connect to this server, the client needs to send another DNS lookup, this time for server manic. After the DNS server answers (manic has IP 128.119.240.90) the client sends a HTTP GET request to download the second image.

This server however responds that the image is located on a different server, and that the client should download the image from <http://caite.cs.umass.edu/>. This is done using a HTTP 302 response message.

The client then contacts the DNS server again to get the IP address of caite. Unfortunately, caite has the same IP address as manic, being 128.119.240.90. Once the client knows the IP of caite, it sends a final GET request to download the second image from this server

## A real world example

**Take a look at the conversations. What do you notice?**

There are a lot of different protocols, such as DNS, ICMP, TCP, ARP, HTTP, EPM, SSDP,... When you go to statistics and then to Conversations, there are different tabs: UDP, IPv4, IPv6, Ethernet and TCP

**Take a look at the protocol hierarchy. What are some interesting protocols listed here?**

Go to statistics and then to protocol hierarchy. TCP is one of the most common, also IPv4 and SSH. SSH is a part of the TCP.

**Can you spot an SSH session that got established between 2 machines? List the 2 machines. Who was the SSH server and who the client? What ports were used?**

SSH is located at port 22, you can find them by this command in the searchbox `tcp.port == 22`. Check SYN to know Client -> Server, in this case, client is 172.30.128.10 and the server is 172.30.42.2. Server-port is usually 22. The Client port is a random high port (more then 1024) assigned dynamically.

**Some cleartext data was transferred between two machines. Can you spot the data? Can you deduce what happened here?**

Cleartext data is often found in unencrypted protocols such as HTTP. Go to Analyze, Follow and HTTP Stream. Someone interacted with a web-based command execution interface on <www.insecure.cyb>. In the POST request to /exec, we see: `{"cmd":"ip a"}`, this means the user executed the command `ip a`. This command is an injection vulnerability. If an attacker can send arbitrary commands to `/exec`, they could execute system commands, escalate privileges, extrafiltrate sensitive data,...

What happened here? A user accessed the web interface at <www.insecure.cyb>, they used the command execution feature to run `ip a` and retrieve the server's network information. The server returned network detailsin cleartext JSON response. 

**How to look for traces of actual attackers?**

Look for exploits & attacks: `http.request.method == "POST" && http contains "cmd="`

Look for unauthorized access: `ftp.request.command == "USER" || ssh` or `icmp || tcp.flags == 0x0002`

Look for suspicious conncections: `tcp.port > 1024 && !(tcp.port == 443 || tcp.port == 80)`

Tip: Using a display filter might be useful: <https://wiki.wireshark.org/DisplayFilters> can give you a hint on how to filter on a subset of the captured packets.

## Extra information

### Active vs passive FTP

In active mode the server initiates the connection to the client for the DATA Channel. In passive mode, the client initiates is. In active mode port 20 is used on the FTP server. In passive mode a random port is used.
