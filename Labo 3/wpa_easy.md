# WPA easy

WPA = WiFi Protected Access

You can open a `cap`-file with `aircrack-ng` in Kali Linux with the command: `aircrack-ng wpa-easy-01.cap`.

## What is the BSSID and ESSID of the wireless network?

BSSID: 00:0F:3D:A7:87:8C

ESSID: HOGENT_WPA

## How many 4-way handshakes does this capture file contain?

There's only 1 handshake:

![handshake](/images/handshake.png)

## What is the WPA password (as string)?

First go to the directory where the file rockyou.txt is located on Kali. To know the exact location, use the command: `locate rockyou`

Go to the location with: `cd /usr/share/wordlists/`

Then unzip the file with: `gzip -d rockyou.txt.gz`

After the unzip, I've gone to the root again and copied the unzipped file to the directory where my `.cap`-file is located.

`cp /usr/share/wordlists/rockyou.txt`

Now you can crack the password:

`aircrack-ng -w rockyou.txt wpa-easy-01.cap`

The password in this case is: `KEY FOUND! [ together ]`

## What command did you use to find this information?

`aircrack-ng -w rockyou.txt wpa-easy-01.cap`

## Which wordlist did you use?

`rockyou.txt`
