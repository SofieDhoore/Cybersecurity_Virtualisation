# Port Scanning

Experimenting with `nmap`, we use the Kali Linux. Go to the terminal and use the command: `nmap scanme.nmap.org`.

The following came out of the terminal:

```console
(osboxes㉿osboxes)-[~]                                                                                                                                                                                                                  
└─$ nmap -d scan.me.nmap.org
Starting Nmap 7.95 ( https://nmap.org ) at 2025-07-21 05:25 EDT
PORTS: Using ports open on 0% or more average hosts (TCP:1000, UDP:0, SCTP:0)
--------------- Timing report ---------------
  hostgroups: min 1, max 100000
  rtt-timeouts: init 1000, min 100, max 10000
  max-scan-delay: TCP 1000, UDP 1000, SCTP 1000
  parallelism: min 0, max 0
  max-retries: 10, host-timeout: 0
  min-rate: 0, max-rate: 0
---------------------------------------------
Initiating Ping Scan at 05:25
Scanning scan.me.nmap.org (50.116.1.184) [4 ports]
Packet capture filter (device eth1): dst host 10.0.2.15 and (icmp or icmp6 or ((tcp or udp or sctp) and (src host 50.116.1.184)))
We got a TCP ping packet back from 50.116.1.184 port 80 (trynum = 0)
Completed Ping Scan at 05:25, 0.01s elapsed (1 total hosts)
Overall sending rates: 383.40 packets / s, 14569.16 bytes / s.
mass_rdns: Using DNS server 192.168.1.1
Initiating Parallel DNS resolution of 1 host. at 05:25
mass_rdns: 0.17s 0/1 [#: 1, OK: 0, NX: 0, DR: 0, SF: 0, TR: 1]
Completed Parallel DNS resolution of 1 host. at 05:25, 0.17s elapsed
DNS resolution of 1 IPs took 0.17s. Mode: Async [#: 1, OK: 1, NX: 0, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating SYN Stealth Scan at 05:25
Scanning scan.me.nmap.org (50.116.1.184) [1000 ports]
Packet capture filter (device eth1): dst host 10.0.2.15 and (icmp or icmp6 or ((tcp or udp or sctp) and (src host 50.116.1.184)))
Discovered open port 443/tcp on 50.116.1.184
Discovered open port 443/tcp on 50.116.1.184
Increased max_successful_tryno for 50.116.1.184 to 1 (packet drop)
Discovered open port 80/tcp on 50.116.1.184
Discovered open port 22/tcp on 50.116.1.184
Discovered open port 80/tcp on 50.116.1.184
Bogus rttdelta: 2803589 (srtt 84918) ... ignoring
Bogus rttdelta: 2803655 (srtt 84852) ... ignoring
Bogus rttdelta: 2867340 (srtt 84918) ... ignoring
Bogus rttdelta: 2867406 (srtt 84852) ... ignoring
Completed SYN Stealth Scan at 05:25, 19.01s elapsed (1000 total ports)
Overall sending rates: 158.24 packets / s, 6960.05 bytes / s.
Nmap scan report for scan.me.nmap.org (50.116.1.184)
Host is up, received reset ttl 255 (0.022s latency).
Other addresses for scan.me.nmap.org (not scanned): 2600:3c01:e000:3e6::6d4e:7061
rDNS record for 50.116.1.184: ack.nmap.org
Scanned at 2025-07-21 05:25:02 EDT for 19s
Not shown: 996 filtered tcp ports (no-response)
PORT    STATE  SERVICE REASON
22/tcp  open   ssh     syn-ack ttl 255
80/tcp  open   http    syn-ack ttl 255
113/tcp closed ident   reset ttl 255
443/tcp open   https   syn-ack ttl 255
Final times for host: srtt: 22492 rttvar: 41243  to: 187464

Read from /usr/share/nmap: nmap-protocols nmap-services.
Nmap done: 1 IP address (1 host up) scanned in 19.49 seconds
           Raw packets sent: 3012 (132.456KB) | Rcvd: 20 (820B)
```

`nmap` doesn't scan all the 65535 ports, it only scanned 995 ports. With the command `nmap -p 1-65535 scan.me.org` you can scan all the ports.

```console
┌──(osboxes㉿osboxes)-[~]
└─$ nmap -p 1-65535 scanme.nmap.org                                                      
Starting Nmap 7.95 ( https://nmap.org ) at 2025-05-10 04:27 EDT
Nmap scan report for scanme.nmap.org (45.33.32.156)
Host is up (0.00072s latency).
Other addresses for scanme.nmap.org (not scanned): 2600:3c01::f03c:91ff:fe18:bb2f
All 65535 scanned ports on scanme.nmap.org (45.33.32.156) are in ignored states.
Not shown: 65535 filtered tcp ports (net-unreach)

Nmap done: 1 IP address (1 host up) scanned in 15.84 seconds
```

Only TCP ports are listed, to scan the UDP-ports, use the command: `sudo nmap -sU scanme.nmap.org`

```console
┌──(osboxes㉿osboxes)-[~]
└─$ sudo nmap -sU scanme.nmap.org
[sudo] password for osboxes: 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-05-10 05:17 EDT
Nmap scan report for scanme.nmap.org (45.33.32.156)
Host is up (0.018s latency).
Other addresses for scanme.nmap.org (not scanned): 2600:3c01::f03c:91ff:fe18:bb2f
Not shown: 999 open|filtered udp ports (no-response)
PORT    STATE SERVICE
123/udp open  ntp

Nmap done: 1 IP address (1 host up) scanned in 12.05 seconds
```

To speed up the process you can scan only the 20 most common ports with the command: `sudo nmap -sU --top-ports 20 scanme.nmap.org`. It took 3.74 seconds.

```console
┌──(osboxes㉿osboxes)-[~]
└─$ sudo nmap -sU --top-ports 20 scanme.nmap.org
[sudo] password for osboxes: 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-05-10 05:44 EDT
Nmap scan report for scanme.nmap.org (45.33.32.156)
Host is up (0.036s latency).
Other addresses for scanme.nmap.org (not scanned): 2600:3c01::f03c:91ff:fe18:bb2f

PORT      STATE         SERVICE
53/udp    open|filtered domain
67/udp    open|filtered dhcps
68/udp    open|filtered dhcpc
69/udp    open|filtered tftp
123/udp   open          ntp
135/udp   open|filtered msrpc
137/udp   open|filtered netbios-ns
138/udp   open|filtered netbios-dgm
139/udp   open|filtered netbios-ssn
161/udp   open|filtered snmp
162/udp   open|filtered snmptrap
445/udp   open|filtered microsoft-ds
500/udp   open|filtered isakmp
514/udp   open|filtered syslog
520/udp   open|filtered route
631/udp   open|filtered ipp
1434/udp  open|filtered ms-sql-m
1900/udp  open|filtered upnp
4500/udp  open|filtered nat-t-ike
49152/udp open|filtered unknown

Nmap done: 1 IP address (1 host up) scanned in 3.74 seconds
```

To detect which operating system and services are running on these ports, use the command `nmap -A scanme.nmap.org`.
In my case the scanning gave up, maybe because the `-A` is to aggresive, I've got this output:

```console
┌──(osboxes㉿osboxes)-[~]
└─$ nmap -A scanme.nmap.org                                                                           
Starting Nmap 7.95 ( https://nmap.org ) at 2025-05-10 05:50 EDT
Warning: 45.33.32.156 giving up on port because retransmission cap hit (10).
```

I've used the following command: `sudo nmap -sS -sV -O -p 22,80,9929,31337 scanme.nmap.org` and got the following output:

```console
┌──(osboxes㉿osboxes)-[~]
└─$ sudo nmap -sS -sV -O -p 22,80,9929,31337 scanme.nmap.org                                          
[sudo] password for osboxes: 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-05-10 06:10 EDT
Nmap scan report for scanme.nmap.org (45.33.32.156)
Host is up (0.12s latency).
Other addresses for scanme.nmap.org (not scanned): 2600:3c01::f03c:91ff:fe18:bb2f

PORT      STATE SERVICE    VERSION
22/tcp    open  ssh        OpenSSH 6.6.1p1 Ubuntu 2ubuntu2.13 (Ubuntu Linux; protocol 2.0)
80/tcp    open  http       Apache httpd 2.4.7 ((Ubuntu))
9929/tcp  open  nping-echo Nping echo
31337/tcp open  tcpwrapped
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Aggressive OS guesses: Oracle Virtualbox Slirp NAT bridge (88%), Dell PowerVault 705N NAS appliance (87%), IBM AIX 4.3 (86%), Denon AVR-2113 audio receiver (86%), QEMU user mode network gateway (86%), Ricoh Aficio BP20N printer (86%), AT&T BGW210 voice gateway (85%), FireBrick FB2700 firewall (85%), Huawei VRP 5.160 (85%)
No exact OS matches for host (test conditions non-ideal).
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 15.12 seconds
```

To get to know the vulnerabilities on the detected ports, you can run a script `vulners`, for more information: `https://github.com/vulnersCom/nmap-vulners`. To detect the vulnerabilities for the SSH server, use the following command: `nmap -sV --script vulners -p 22 scanme.nmap.org`
