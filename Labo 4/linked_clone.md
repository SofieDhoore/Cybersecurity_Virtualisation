# Create a linked clone of the Windows VM

Go to your VM you want to clone. Click on the VM and right click on `Current State`, then you can choose the option `clone`. When you've clicked next, be sure you select linked clone.

Before starting the clone, look at the result.

## Where is the base VDI stored? Where is/are the delta file(s) stored?

The base VDI is stored here: `C:\Users\sofie\VirtualBox VMs`. It's in the directory with the original VM.

The delta file is stored in the directory of the linked clone. `C:\Users\sofie\VirtualBox VMs\Windows 10 Clone`. The delta file is `.vdi`-file that's changing versus the base file.

## What happened to the original VM?

Nothing happened to the base file. You can use it as before.

## What is the relationship between linked clones and snapshots?

A linked clone is based on a snapshot. The clone uses the base VDI + snapshot as a read-only. It writes it own changes in it own delta file.
