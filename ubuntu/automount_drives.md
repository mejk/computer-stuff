# Automounting HDs/SSD etc

First find out what file systems are available

```
lsblk
```
The list could, for example, look like the following:
```
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
loop0    7:0    0 295.7M  1 loop /snap/vlc/2344
loop1    7:1    0  43.3M  1 loop /snap/snapd/14295
loop2    7:2    0  55.5M  1 loop /snap/core18/2284
sda      8:0    0 931.5G  0 disk 
├─sda1   8:1    0   512M  0 part /boot/efi
└─sda2   8:2    0   931G  0 part /
sdb      8:16   0 931.5G  0 disk 
├─sdb1   8:17   0   512M  0 part 
└─sdb2   8:18   0   931G  0 part 
```
Here, the disk `sdb` has not been mounted.

If that shows drives, we can then get their names and IDs
```
sudo blkid
```
Here, 
```
/dev/sdb1: UUID="663F-3903" TYPE="vfat" PARTLABEL="EFI System Partition" PARTUUID="aef7e5ea-73b4-4d80-a3b9-eb9d70606cc5"
/dev/sdb2: UUID="829523b0-1973-4488-96a0-6e078bf2c7d5" TYPE="ext4" PARTUUID="97881f34-1c99-48f3-ae0e-60f89dd3d835"
```
We want to automount `/dev/sdb2` to `/data`. It is of type `ext4`, that is, standard Linux.

Next, we need to make a mountpoint. Here, the drive 'sdb' will be mounted to '/data'.
```
sudo mkdir /data
```
To automount the drive to `/data`, we need to edit `/etc/fstab`. For example,
```
sudo vi /etc/fstab
```
We add the following line (taking the UUID and type from above):
```
UUID=829523b0-1973-4488-96a0-6e078bf2c7d5  /data  ext4  defaults  0     2
```
The option `defaults` gives the users read and write access. The last digit tells if the file system should be checked: 0=no, 1=root system, 2=check (for other file systems).

After saving the file, test if it works:
```
sudo mount -a
```

