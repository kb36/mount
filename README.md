Description: mount Linux partitions permanantly in ubuntu

1) sudo fdisk -l

In my case, output is
Disk /dev/sda: 232.9 GiB, 250059350016 bytes, 488397168 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: 3946D2B0-4554-4AF4-A7BC-F37FACA65B63

Device         Start       End   Sectors   Size Type
/dev/sda1       2048   1050623   1048576   512M EFI System
/dev/sda2    1050624 438212607 437161984 208.5G Linux filesystem
/dev/sda3  438212608 488396799  50184192    24G Linux swap

Disk /dev/sdb: 931.5 GiB, 1000204886016 bytes, 1953525168 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 4096 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes
Disklabel type: dos
Disk identifier: 0x91f59915

Device     Boot Start        End    Sectors   Size Id Type
/dev/sdb1        2048 1953520064 1953518017 931.5G 83 Linux

2) I would like to have backup in the path: /mnt/backup
create directoty: sudo mkdir -p /mnt/backup
3) ls -l /dev/disk/by-uuid
In my case output is:
total 0
lrwxrwxrwx 1 root root 10 May  8 11:26 2038b5cb-5f90-4356-9d64-a9ccb42f3703 -> ../../sda2
lrwxrwxrwx 1 root root 10 May  8 11:26 3bf4bc37-6903-4309-be0b-1e96bdb56e0b -> ../../sda3
lrwxrwxrwx 1 root root 10 May  8 11:26 70E7-E991 -> ../../sda1
lrwxrwxrwx 1 root root 10 May  8 11:26 d002bed4-5136-4b49-b76d-cd31802e4e95 -> ../../sdb1

4) I am going to mount the sdb1 partition. take backup of /etc/fstab.
sudo cp /etc/fstab ~/Desktop/fstab
5) sudo vi /etc/fstab
Add line
UUID=d002bed4-5136-4b49-b76d-cd31802e4e95 /mnt/backup ext4 defaults 0 0
at the end.
6) sudo mount -a
reboot the system.

If there are permission issues, change permissions using chmod, chown as you would regularly do.
