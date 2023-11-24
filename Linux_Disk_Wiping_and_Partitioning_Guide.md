# Disk Wiping and Partitioning Guide

This guide provides instructions for securely wiping a disk and creating a new partition formatted with exFAT. 

## Listing Disks

First, list all disks to identify the one you want to work with: 

```
sudo fdisk -l
```

## Secure Data Wiping with DoD 5220.22-M Standard

The DoD 5220.22-M standard requires multiple passes of overwriting with specific patterns and a final verification. 

```
shred -n 3 -z /dev/sdX
```

## Creating a New Formatted Partition with exFAT

exFAT (Extended File Allocation Table) is a filesystem designed for flash storage like USB drives and SD cards. It's used for its ability to handle large files (over 4GB), which FAT32 can't, and for its compatibility across Windows, macOS, and many Linux distributions. Ideal for use in a storage device intended as a portable drive, exFAT ensures seamless data transfer and storage of large files across different operating systems. 
 
To create a new partition: 

```
fdisk /dev/sdX
d # to delete partitions
n # to create partitions
p # primary
1 # first partition
# Press Enter for the first sector
# Press Enter for the last sector
S (or Y) # to remove any other partition signature
t # to choose partition type
7 # for HPFS/NTFS/exFAT
w # to write the changes
```

Finally, format the partition with exFAT: 

```
sudo mkfs.exfat /dev/sdX1 # to format
```

> Remember to replace /dev/sdX and /dev/sdX1 with the correct identifiers for your disk and partition.
