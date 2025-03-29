# Communication between host and VM

The simplest approach is Bridged Adapter.

- Set up the VirtualBox network adapter to Bridge Mode so that VMs get an IP address from the same network as the host.
- This allows direct connectivity between the host and the VMs without port forwarding

## Setup a new Host-Only Network

Go to Tools and select Network. There you can set up a new Host-Only network simply by clicking Create. There you can set up the network-range to `192.168.100.1` and click Apply. On the the next tab you can enable or disable the DHCP service.

## Create a VM for the Debian router

I've downloaded a Debian VM on <https://www.debian.org/releases/bookworm/debian-installer/> and choose the `amd64`. I've set up the non-graphical install.

## Prepare the VM

I've set up 2 adapters, a NAT and a Host-Only.

## Router configuration

Access to root with `sudo su -`, give the password from your user. After setting up a routing-script and running the script, I could make a connection with the Kali Linux & Windows 10 VM. There was first some trouble to connect but I needed to select the Virtual Box Host Only Adapter #2 for the two VM's.

To make connection with internet & ping the router, you need to start the Debian CLI router in VirtualBox. After that start up the other VM's, now you can also ping both VM's to each other.

### SSH connection

First start up your Debian CLI and login as root. Go to Windows prompt and typ `ssh [username]@[ip-vm-router]`, enter password and now you've made connection the VM-router from your hostmachine. And you can now copy-paste easily from your host.
  