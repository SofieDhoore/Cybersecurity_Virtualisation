# VBoxManage

First, locate the VBoxManage executable on your host system. In my case it's located here: `C:\Program Files\Oracle\VirtualBox\VBoxManage.exe`.

You can use it with the command prompt in Windows, for example if you want to show all the VMs on your host, use the command:
`VBoxManage list vms`.

To start a VM, use the command: `VBoxManage startvm "name_vm"`

```console
C:\Users\sofie> VBoxManage startvm "KaliLinux"
Waiting for VM "KaliLinux" to power on...
VM "KaliLinux" has been successfully started.
```

To change the amount of virtual RAM to your Kali VM: `VBoxManage modifyvm KaliLinux --memory 2048`.

To change the amount of video RAM to you Kali VM: `VBoxManage modifyvm KaliLinux --vram 64`.

To take a snapshot: `VBoxManage snapshot KaliLinux take test --description="Test snapshot of Kali VM`.

To delete the snapshot again: `VBoxManage snapshot KaliLinux delete test`.
