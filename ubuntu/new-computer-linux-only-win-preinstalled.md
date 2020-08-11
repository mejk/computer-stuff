# New computer came with windows pre-installed but you want Linux only

Works also if you just want to wipe out Windows from your old computer and make it Ubuntu (Linux) only. 

<tt>Updated: Wed 29 Jul 22:58:32</tt>

- Tested:
  - Lenovo Yoga X11
  - Dell XPS 13
  - Alienware R8 desktop with NVIDIA RTX 2070 Super
  - MSI GS65 with NVIDIA GTX 1070
-------------------------------

## Preparations

- **Need:** 1 USB for creating a bootable USB for your Linux installation. If you want (can be done later), another USB for creating Windows installation media.
- Get your favourite Linux distro and create a bootable USB. These instructions should work with any of the Ubuntu flavours, but here're the precise ones used in these cases (the computers listed above):
  - [Ubuntu Budgie 20.04 LTS](https://ubuntubudgie.org/downloads/)
  - [KDE Neon](https://neon.kde.org/download). Here, Ubuntu 18.04 LTS-based version was used. A new one based on 20.04 LTS should be available soon
  - Choose an image writer for creating a bootable USB. There are a lot of options but here Unetbootin was used.
    - [Unetbootin](https://unetbootin.github.io/). For Windows, Linux and Mac
- In case you want to install Windows in a Virtual machine, get an image file for Windows and create a bootable USB. 
  - [Windows installation media](https://support.microsoft.com/en-ca/help/15088/windows-10-create-installation-media). This needs to be done on a windows computer. This is also the reason why we get the Windows license key as instructed below.  
- **Extract the Windows licence key** so that you can use it for installing Windows in Virtual Machine (or in case you want to get back to Windows). Here's how:
  - [How to find your Windows licence key](windows-licence-key.md)

## Notes on the specific systems used here:

- The instructions below are based on installing Ubuntu Budgie 20.04 LTS and KDE Neon 18.04 on Dell XPS, Lenovo X1 Yoga and Alienware R8 with Nvidia 2070 Super graphics card. Here's how it worked on the different computers:
  - Dell XPS 13 (KDE Neon 18.0 4LTS and Ubuntu Budgie 20.04 LTS): everything worked out of the box
  - Lenovo X1 Yoga (Ubuntu Budgie 20.04 LTS): everything worked out of the box including the stylus
  - Alienware R8 with Nvidia 2070 Super (Ubuntu Budgie 20.04 LTS) : The discrete GPU create some problems are discussed below, but it worked out easily.
  - MSI GS65 with NVIDIA 1070 (KDE Neon 18.04 LTS and Ubuntu Budgie 20.04 LTS): With 20.04 LTS everything worked out, but with 18.04 LTS there were issues with the Wifi card.

## Start the computer

Windows does its usual set up routine. If you plan to wipe Windows 10 out after getting the keys, just do the minimal setup to get in.

**1. Start Windows:**
  - No need to run updates
  - Get the Windows 10 license key (see **Preparations** above)
  - Get the system details and possible service tags if applicable (might be good idea for warranty etc.) 

**2. Reboot and go into the Bios setup. Check/do the following:**
  - SATA operation: It is typically set as RAID on. Change to AHCI. 
    - You will get a warning message. 
  - Secure boot: Typically set as 'Enabled'. Change to 'disabled'
    - You will get a warning message. 
  - Firmware TPM (Trusted Platform Module). Can be left Enabled or Disabled. Most likely, you need to disable it. If interested, see this article: [More info about TPM](https://www.linux-magazine.com/Issues/2018/206/Trusted-Platform-Module)
    - On Alienware R8 TPM had to be disabled.
  - Check that 'Enable USB boot support' is on on. Not all systems have this option. 
  - Save and exit
**3. Reboot.**
  - If you want to be sure that everything went ok, let the system to reboot to Windows. 
**4. If that worked, insert the installation USB and reboot.**
  - If the system boots to Windows, then keep the USB on and reboot and either
     - Enter Bios again and set the boot order to USB first or
     - Enter 'Startup options' and select the USB.
**5. You should now be running Linux from your USB.** If everything looks and works well (and connects to Internet), you can click 'Install'. 
  - Notes:
    - 'Normal installation' is probably a good idea
    - It may be a good idea to select 'Download updates while installing' and 'Install third-party software for graphics and Wi-Fi hardware' from 'Other options'. 
    - The critical step is the next one called  'Installation type'. It allows for a dual boot installation or to erase and format the the disk and install Linux. The latter wipes out whatever there is on the drive. This is what will be done here. Instructions for dual boot are found here: [How to install Windows / Linux dual boot]. There is also an option 'Something else'. If you have specific needs and know what you are doing, then that is for you. 
    
**6. When the installation is done, it will ask you to reboot (=do it).**
- If all went well, you are now in your newly installed system. 
  
If all that worked out, you are done and just need to install whatever software you want. 
 
## Potential problems 

With Alienware R8 with Nvidia 2070 Super, there was an issue. See the next point: 
  - Potential problem: Discrete graphics (when using the latest cards). This may need to you 
    - In Ubuntu 20.04 LTS you can enter the bootloader by pressing the ESC button when booting.
      - Select: 'Advanced options for Ubuntu'
      - The option that worked was to select to boot in the 'Failsafe' mode. 
  
- Run the software updater to update your system. Before rebooting:
 - It is a good idea to check the software sources in your Software updater (see 'Settings'). 
   - Under 'Other Software' select 'Canonical Partners' (no need to pick the Source Code option unless there is some very specific reason).
   - If you have discrete GPU: Check what you have under 'Additional Drivers'. The updated pulled the correct driver for my Nvidia 2070 Super so nothing needed to be done. You can also double check your driver by opening a terminal window and giving the command `ubuntu-drivers devices`. In my case, this confirmed that the driver was indeed updated properly    

- If the graphics problem continues, you need to do the following two things:
  1. Enter the bootloader and add
  ```
  nomodset 
  ```
  at the end of the line that starts `linux` and remove or comment out
  ```
  $vt_handoff
  ```
  on that same line.
  2. In addition, comment out or remove the line
  ```
  gfxmode $linux_gfx_mode
  ```
    
## Potential problems with discrete GPU:
- If the screen is unreadbale and garbled, reboot and select the option 'with safe graphics'. 
  - Note this was needed on to boot the Ubuntu 20.04 LTS USB on Alienware R8 with Nvidia 2070 Super

