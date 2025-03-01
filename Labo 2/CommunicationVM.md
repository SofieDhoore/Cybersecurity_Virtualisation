# Make communication possible between both VMs

Now we want to capture all the traffic from our Windows 10 client using our Kali VM. In order to do so, we have to adjust the network settings so that both VMs can communicate with eacheother.

In the default NAT mode, this is impossible, as every VM is connected to a separate virtual network. We are not going to add any additional interfaces to our VMs.

Experiment with the different network modes (NAT, NAT Network, Bridged, Internal, Host-Only) and try to answer the following questions.

1. Can both VMs communicate with each other? If communication is possible, you should be able to ping the Windows 10 VM from your Kali VM.
2. Can both VMs access the internet? Is NAT being used, and if so, which router in the network handles the translation?

Final goal: configure both VMs in such a way that they can ping to each other, and both VMs should have internet access.
