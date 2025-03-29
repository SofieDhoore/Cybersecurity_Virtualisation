# Capture Telnet and SSH Traffic

We first make a telnet client on Windows 10 VM.

- Click Start
- Open the Control Panel and click on Programs
- Click on "Turn Windows Featurs on or off"
- Select the Telnet Client option and click OK

To go into Telnet, simply go to the Command Prompt and typ `telnet`, typ `q` to quit.

After that go to Kali and install the DARPA telnet protocol server: `sudo apt update && sudo apt install telnetd -y`.

Login as root in Kali: `su`

Show all the folders: `ls /`

Edit the file `/etc/inetd.conf`, you can enter it with `nano /etc/inetd.conf`, remove `#<off>#` at the line with telnet. Finally restart inetd with `/etc/init.d/inetutils-inetd restart`

```console
root㉿osboxes)-[/etc]
└─# /etc/init.d/inetutils-inetd restart
Restarting inetutils-inetd (via systemctl): inetutils-inetd.service.
```

## Telnet Capture Instructions

Open Wireshark on Kali and capture traffic on `eth0`. In Windows 10 VM write in commandline: `telnet [ip-address Kali] 23` and enter the Kali Linux with your account. Look at all the maps in the home folder `ls`.

## Questions related to your Telnet capture

1. Can you filter on the IP address of the server? Yes, by typing `ip.addr == [ip-address telnetserver]`
2. What was the (TCP) destination port that you have connected to? What was the client port used by your client (for this session)? Clientport is 50340, the Destination port is 23.
3. Right click, and try to re-assemble the entire TCP stream of your connection. Describe what you can deduct from the displayed information. I can see all the data sent over telnet, including login and password.
4. Is setting up a Telnet connection method to e.g. a Cisco router or switch a good practice? No, because you can see the login details.

## SSH Capture Instructions

First start ssh on Kali Linux by this command `sudo systemctl start ssh`. Or `sudo systemctl enable ssh` when you want it to be enabled all the time. Open a command prompt in Windows and use the command `telnet [ip-address Kali] 22`. Start capturing with Wireshark on Kali. Also make a connection in a new terminal by using this command `ssh osboxes@[ip-address Kali]`.

## Questions related to your SSH capture

1. What was the (TCP) destination port that you have connected to? What was the client port used by your client (for this session)? The clientport is 50389, the destination port is 22.
2. Right click, and try to re-assemble the entire TCP stream of your connection. Describe what you can deduct from the displayed information. Most information is not readable. This is because SSH encrypts all communication between server and client. The only thing that is readable is the SSH version used by both parties.
