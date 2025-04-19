# Experiment with snapshots

Shutdown the virtual machine and take a snapshot. Start the virtual machine and create a file with some content on the Desktop. I've created a file named 'Dagboek'.

## Take a snapshot

### Where is the base VDI stored? What size (in MB) is it?

C:\Users\sofie\VirtualBox VMs\LinuxMint21

14,213.12 MB of 14 GB

### Where is the delta file stored? What size (in MB) is it?

C:\Users\sofie\VirtualBox VMs\LinuxMint21\Snapshots

289.792 MB of 0.2897 GB

## Restore the snapshot

### Is the textfile still present on the Desktop? Why (not)?

Yes, the file Dagboek is still there. Restoring a snapshot is generally the reverse of a creation process.
Restore undoes all changes since creating snapshot. You return to state VM when creating snapshot. Quite fast (delete delta file).

### Does this change anything to the base VDI?

No, the base vdi didn't change, the date and amount is still the same.

### Does this remove the delta file?

Yes, the delta file is replaced by the restored vdi.

## Delete the snapshot

### Is the textfile still present on the desktop? Why (not)?

The textfile is still present. It's because the snapshot has been deleted after making the textfile.

### Do you still have the delta file? Why (not)?

No, the delta file has been deleted by deleting the snapshot. Because the changes from the delta file are integrated (merged) with the base vdi-file.
