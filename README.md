# Random computer stuff

- Random notes on various computer issues, installation etc.  
- The installations described on the pages have been tested but mileage may vary.

- **USE AT YOUR OWN RISK!** *If you end up wiping out your data or bricking your computer, you have been warned.*

----------------------

## Before we start: Here are some sites for Linux-related news etc:
Lots of stuff below is based on these sources. 

- [It's FOSS](https://itsfoss.com)
  - [It's FOSS has a lot of great How-tos.](https://itsfoss.com/category/how-to/)
- [OMG Ubuntu](https://www.omgubuntu.co.uk/)
- [nixCraft](https://www.cyberciti.biz/)
- [Linux Insider](https://linuxinsider.com/)
- [Linux Magazine](https://www.linux-magazine.com)

---------------------

## How to...

- [Wipe out Windows and install Ubuntu only](ubuntu/new-computer-linux-only-win-preinstalled.md)
  - You can always install Windows in VirtualBox
- [Install dual boot Windows 10 / Ubuntu 20.04 LTS](dual-boot-ubuntu-Windows10.md)
- [Quick installation of software on Ubuntu 20.04 LTS](ubuntu/fast-software-installation.md)

## General cross-platform software: Linux, Windows & Mac

- [Cross platform (Linux, Windows, Mac) software](cross-platform-software.md)
  - Word processors, reference managers, graphics, communication, programming, etc.

## VNC, SSH, etc

- [VNC client and server installation](vnc-installation.md)
- [VNC client and server basic use](vnc-how-to-use.md)
- [SSH keys, config files and ssh agents](ssh-keys.md)

## Ubuntu

- [Installation of CUDA and Nvidia drivers & TensorFlow (Ubuntu 20.04 LTS)](ubuntu/cuda-and-nvidia-drivers.md)
  - TensorFlow 2 with & without GPU support using Docker.
- [Quick installation of software on Ubuntu 20.04 LTS](ubuntu/fast-software-installation.md)
- [Word processors with GUI: WPS Office and LibreOffice](ubuntu/word-processors-with-gui.md)
  - WPS Office with the extra fonts installed (instructions provided) is an excellent MS Office replacement with very high degree of compatibility.
  - LibreOffice connects well with JabRef reference manager, supports LaTeX math (via a plugin) and has great support for scalable vector graphics.
- [Ubuntu/Linux tips and tricks](ubuntu/ubuntu-tips-and-tricks.md)
  - Mish-mash of a lot of stuff.

- Java. How to check your current Java version? Like this: `java -version`. You may have/want different Java versions (JRE/Development Kit) on your computer.   Here's how to switch between them:
   - `sudo update-alternatives --config java`

- Install [Jupyter Notebooks / JupyterLab](ubuntu/jupyter-notebooks.md)

- Fix the problem [kswapd0 takes 100% of CPU](ubuntu/swap.md)

- Mapping the tablet on one screen only in dual/multiple screen setup. The procedure below is from here : [Ubuntu Linux - Map Wacom to one screen when using multiple screens](https://feldspaten.org/2017/05/06/ubuntu-linux-map-wacom-to-one-screen-when-using-multiple-screens/):
  Get primary display (or any other using xrandr):
  ```
  xrandr | grep 'primary'
  ```
  Get the stylus id:
  ```
  xinput | grep -i Wacom
  ```
  Do the mapping - for XY substitute the device id number from above (DP-1 was the main screen, replace with yours):
  ```
  xinput map-to-output XY DP-1
  ```
  
### Clear cache and swap

Execute the following as root:
```
sync; echo 3 > /proc/sys/vm/drop_caches 
```
- more: [How to Clear RAM Memory Cache, Buffer and Swap Space on Linux](https://www.tecmint.com/clear-ram-memory-cache-buffer-and-swap-space-on-linux/)

  
### xrdp fails on 20.04
This worked: comment out the two last lines in `/etc/xrdp/startwm/sh` and add one
```
# test...
# exec..
startxfce4
```


## Dual boot problems

It may happen (well... happened to me once) that after a Bios update the system boots directly to Windows and it appears that Grub has been lost altogether. In my case, that's what happened. What helped was the advice from [this link](https://www.reddit.com/r/kde/comments/auctv3/kde_neon_no_boot_manager/). In brief: 
- Boot from live USB.
- Check if `boot-repair` is already part of the live USB (check from the Program Menu). If not, then
- Open terminal and type 
```
sudo apt-add-repository ppa:yannubuntu/boot-repair
sudo apt-get update
sudo apt-get install -y boot-repair
```
- Then find `boot-repair` from the Program Menu and run it. I used the recommended process.
- This fixed it on Lenovo C940.

## Windows

- [How to find your Windows licence key](windows-licence-key.md)
  - For example: if you wipe out Windows, you may still want to install it in VirtualBox and then you need the key (and you have already paid for it)
- [How to remove BitLocker](windows/bitlocker.md)
  - This may be important when creating a dual boot computer.
- WSL (Ubuntu shell) and GUI software
  - NOTE: WSL and WSL2 are different. WSL will work easily on pretty much any Windows 10 system, WSL2 brings in a lot of great things but at this time (summer 2020) it is not for everyone.
  - [WSL and WSL2 from Microsoft](https://docs.microsoft.com/en-us/windows/wsl/install-win10)
  - [WSL and WSL2 from OMG Ubuntu](https://www.omgubuntu.co.uk/how-to-install-wsl2-on-windows-10)
  - Check which version of WSL you have: Open Powershell and type `wslconfig /l`
  - GUI apps work great when you install [Vcssrv](https://sourceforge.net/projects/vcxsrv/) or [Xming](https://sourceforge.net/projects/xming/)
  - [OpenSSH in Windows 10](windows/openssh-windows.md)


## Mac OSX
- [Fuzzy and/or jaggedy fonts on external screens](mac/blurry-fonts.md)
