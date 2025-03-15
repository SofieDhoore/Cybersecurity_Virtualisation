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
  