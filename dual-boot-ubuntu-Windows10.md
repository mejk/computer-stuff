# Dual boot Windows & Linux setup

- These steps below have been applied to install dual boot using Ubuntu 20.04 LTS and Windows 10 on both laptops and desktops.

## Preparations:

- **Need:** 1 USB for creating a bootable USB for your Linux installation. If you want (can be done later), another USB for creating Windows installation media.

    
If Windows 10 is (pre-)installed, then you have already paid for the Windows 10 licence. It is a very good idea to get the Windows OEM product key from your computer. Sometimes it is listed in Bios (but not necessarily). Below, the key is extracted from Windows. It is good idea to do that since the licence key is needed in case something goes wrong and you need to reinstall Windows. Even in the case you want to wipe out Windows and have a pure Linux computer, you may want to install a Windows virtual machine inside Linux and for that the Windows licence key is needed. Below are different ways of extracting the licence key depending on if you are in Windows, Linux or Virtual machine.

### Extract the 10 Windows 10 licence key within Windows (tried on MSI, Samsung, Dell XPS) using two possible methods:


1. Open the Windows command window in administrator mode and give the command

```
wmic path softwarelicensingservice get OA3xOriginalProductKey
```

2. or alternatively, use the Windows PowerShell in administrator mode and give the command:

```
powershell “(Get-WmiObject -query ‘select * from SoftwareLicensingService’).OA3xOriginalProductKey”
```

Now you should have the product key. Save it.

### How to extract Windows 10 licence key within Linux using two possible methods:
It is also possible to extract the licence key when logged in Linux.
Open a terminal windows and give one of the two commands:

1.
```
sudo strings /sys/firmware/acpi/tables/MSDM
```

2. or

```
sudo cat /sys/firmware/acpi/tables/MSDM

```

### How to extract Windows 10 licence key within VirtualBox running in Linux (tried on MSI, Samsung, Dell XPS) using two possible methods:
In this case it is assumed that you have already installed Windows 10 in a Virtual Box in Linux.

```
cat "~/VirtualBox VMs/win10/msdm.bin"
```

## Setting up dual boot

Now that we have the licence key saved, let's proceed to setting up dual boot.

### New computer
Although the procedure is the same for installing dual boot on a new or old computer, it is a bit more convenient to do it right away on a new computer since the strorage (SSD or HD) is not fragmented. In addition, an old computer has probably files that need to be backed up just in case something goes wrong.

1. If the computer is new, go through the Windows setup routine. Install possible update as well (this will most likely involve 1 or reboots).
2. Once the setup & possible updates have been completed, remove Bitlocker. 
 - This is how: [How to remove BitLocker](windows/bitlocker.md)
 - Important: Do this before moving to the next step. Otherwise the removal of secure boot becomes more complex.
3. Reboot and enter `BIOS`. In there:
  - Check that the storage (`SATA operation)` is in `AHCI` mode. If not, change to `AHCI`.
  - Disable secure boot 
  - Disable TPM  / Intel Platform Trust Technology
  - Save and reboot
4. Boot back to Windows
  - If all went well, you should be back in Windows now. The next step is to create partition for Linux.
5. Get your favourite Linux distro and create a bootable USB. These instructions should work with any of the Ubuntu flavours, but here're the precise ones used in these cases (the computers listed above):
  - [Ubuntu Budgie 20.04 LTS](https://ubuntubudgie.org/downloads/)
  - [KDE Neon](https://neon.kde.org/download). Here, Ubuntu 18.04 LTS-based version was used. A new one based on 20.04 LTS was released just a few days ago
  - Choose an image writer for creating a bootable USB. There are a lot of options but here Unetbootin was used.
    - [Unetbootin](https://unetbootin.github.io/). For Windows, Linux and Mac

### Older computer

If you have a computer that has been used for some time, run defragging. It may be that Window's own defraggler doesn't do such a great job (if you want more space for your dual boot partition). In some cases these have worked better:
  - Defraggler
  - Auslogics Disk Defrag
  - The most efficient solution has been to reinstall Windows after BitLocker has been removed (see above), then partition the SSD/HD as instructed below. For this, you need to take a backup of your system
      - In this case you need: 
         1. USB for creating Windows installation media.
         2.  [Windows installation media](https://support.microsoft.com/en-ca/help/15088/windows-10-create-installation-media). This needs to be done on a windows computer. This is also the reason why we get the Windows license key as instructed below.

### Create partition for Linux

1. Go to 
```Control Panel` -> `Create and format disk partitions```

  - Choose your C: disk
  - Right click for options. Choose `Shrink Volume`
  - Enter the amount you want to shirnk (that will the size of your new partition
     - For example 700000 gives 700 Gb Linux and leaves about 260 Gb for Windows
  - Select `Shrink`
  - After the reallocation is done, the graphic should show the size of the C: after reallocation and the unallocated space that will be used for Linux.
  
2. Insert the USB drive that contains your Linux distro and rebbot
3. If it boots back to Windows, reboot and enter `bios` and change the boot order such that USB is first. It should now boot from the USB.

### Install Linux

1. You should now be running Linux from your USB. Try that everythihg works, Wifi, trackpad (or mouse), sound, maybe open a few apps like a web browser. If everthing works, go to the next step.

2. Optional: Before choosing to install, open terminal and see the partitions using `df -h`. You should see the new partition that you created. For example, `/dev/nvme0n1p5` or something like that. It is good to do this in case you are not quite sure. 

3. Choose install by click the install icon. 
 - It is usually good to choose the `restricted extras` when the installer ask about the type of installation. This gives extra drivers in case necessary.
 - Choose installation type: Choose `Install Ubuntu alongside Windows Boot Manager` unless there is a reason to do somethig else.
   - The next window should allow you to review the partitions or change them them if you want
 - If all looks good to you, proceed  

4. Once the installation is done, you will be prompted to reboot. Do so.
5. Reboot should take you back to Linux. Go to `Software update` and update the system.
6. After the update is done, it may not be a bad idea to reboot to windows to see that the dual boot works. If that is the case, boot back to Linux and install whatever software need.



## When things go wrong

- Most of the time things just work but sometimes things can go wrong. Below are a few cases than happened + the fixes.

### Potential problem: If the screen freezes (may happen with the latest NVIDIA drivers)

It may happen with the latest graphics/NVIDIA cards (happened with NVIDIA GTX1650M, but there were no troubles with GTX980M, GTX1070M, RTX2070) that the screen freezes on reboot. Installing the latest drivers helps, but first we have to get past the frozen screen. Here is what worked, the info below was collected from this source: 

- [Login freeze after update to 20.04](https://askubuntu.com/questions/1229933/login-freeze-after-update-to-20-04)

1. Upon booting, press `e` for more options on the boot selection screen
2. Add `nouveau.modeset=0` to the end of the `linux` line 
3. Press `F10` to boot.


## Potential problem: Ubuntu 20.04 LTS freezes (sometimes or every time) at the login screen

In this case, the freezing happened at the login screen. 

- This problem seemed to be related to audio drivers. This happened on Lenovo Yoga C940. 
  - This solved the problem: [Ubuntu 20.04 freezes before login screen, no dual boot](https://askubuntu.com/questions/1241151/ubuntu-20-04-freezes-before-login-screen-no-dual-boot). Below is the summary (the above link contains more info and options).

1. When booting, press `e` to edit the boot options. Add 
    ```
     snd_hda_intel.dmic_detect=0
    ```
at the end of the line starting `linux`. 

2. Once the systems boots, login and edit the `grub` file:
```
sudo gedit /etc/default/grub
```
and add `
```snd_hda_intel.dmic_detect=0``` 
at the end of the line that starts
```GRUB_CMDLINE_LINUX_DEFAULT=```

3. Save and give the command
```
sudo grub-mkconfig -o /boot/grub/grub.cfg
```
4. Reboot.

