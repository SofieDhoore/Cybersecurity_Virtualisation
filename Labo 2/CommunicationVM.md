# Make communication possible between both VMs

Now we want to capture all the traffic from our Windows 10 client using our Kali VM. In order to do so, we have to adjust the network settings so that both VMs can communicate with eacheother.

In the default NAT mode, this is impossible, as every VM is connected to a separate virtual network. We are not going to add any additional interfaces to our VMs.

Experiment with the different network modes (NAT, NAT Network, Bridged, Internal, Host-Only) and try to answer the following questions.

1. Can both VMs communicate with each other? If communication is possible, you should be able to ping the Windows 10 VM from your Kali VM.
2. Can both VMs access the internet? Is NAT being used, and if so, which router in the network handles the translation?

Final goal: configure both VMs in such a way that they can ping to each other, and both VMs should have internet access.

## NAT

1. Kali Linux can't communicate with Windows 10. I've got the message "Destination host unreachable"
2. Both VM's can access the internet. The NAT router inside VirtualBox translates the private IPs to the public IP of the host for internet access.

## NAT network

1. Now I can ping Windows with Kali Linux. But I needed to configure the Windows Defender Firewall.
2. Both VM's can access the internet.

## Bridged

1. The VM's can communicate with eachother. The IP address is in the same network as the host.
2. Both VM's can access the internet.

## Internal

1. First it didn't work to ping the Windows VM because for some reason Kali didn't had an IPv4-address. After the set-up it worked.
2. There is no access on the internet for both VM's.

How to set up the Kali IP to get access:

`ip link show` to see if there is eth0 in the list.

`sudo ip addr flush dev eth0` to delete the old IP-configuration.

`sudo ip addr add 192.168.1.20/24 dev eth0` to add an IP address manually.

`sudo ip link set eth0 up` to enable the interface.

`ip a show eth0` to see if the IP address is assigned correctly.

## Host-Only

1. After configuration of the IP on the Windows VM I could ping it from Kali.
2. There is no internet access.

## Remark

The IP addresses from both VM's has to be in the same subnet!
