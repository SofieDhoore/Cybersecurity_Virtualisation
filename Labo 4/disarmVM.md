# Disarm the VM and experiment with anti malware testfile

For this labo we use the Windows Clone VM. First, install 7-zip. I've done this within the commandline as an administrator. I used the command `winget install 7zip.7zip`.

We also need to make the VM vulnerable. Go to Windows Security and then to the Virus & threat protection. Click on manage settings under the Virus & threat protection settings.

![settings](/images/settings.png)

Put off the following protections:

![pretoff](/images/protoff.png)

Go to `https://www.eicar.org/download-anti-malware-testfile` and download the testfile on your VM.

I've got a message which blocks the download, the download was blocked as unsafe by the Windows Defender SmartScreen. To disable this, I needed to go to Windows Settings > Update & Security > Windows Security > App & Browser Control. Go to Reputation-based Protection settings. Click off SmartScreen for Microsoft Edge.

![smartscreen](/images/smartscreen.png)

Now the download wasn't blocked. After a reboot, the file is still present in the download folder. So my VM is still unarmed.
