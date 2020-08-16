# Random computer stuff

- Random notes on various computer issues, installation etc.  
- USE AT YOUR OWN RISK!
- The installations described on the pages have been tested but mileage may vary.

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
- Install dual boot Windows 10 / Ubuntu

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
- [Word processors with GUI: WPS Office and LibreOffice](ubuntu/word-processors-with-gui.md)
  - WPS Office with the extra fonts installed (instructions provided) is an excellent MS Office replacement with very high degree of compatibility.
  - LibreOffice connects well with JabRef reference manager, supports LaTeX math (via a plugin) and has great support for scalable vector graphics.
- [Ubuntu/Linux tips and tricks](ubuntu/ubuntu-tips-and-tricks.md)

- Java. How to check your current Java version? Like this: `java -version`. You may have/want different Java versions (JRE/Development Kit) on your computer.   Here's how to switch between them:
   - `sudo update-alternatives --config java`
- [System tools and related](ubuntu/system-tools.md)
  - git, package managers, application launchers...

## Windows

- [How to find your Windows licence key](windows-licence-key.md)
  - For example: if you wipe out Windows, you may still want to install it in VirtualBox and then you need the key (and you have already paid for it)
- [How to remove BitLocker](windows/bitlocker.md)
  - This may be important when creating a dual boot computer.
- WSL (Ubuntu shell) and GUI software
  - NOTE: WSL and WSL2 are different. WSL will work easily on pretty much any Windows 10 system, WSL2 brings in a lot of great things but at this time (summer 2020) it is not for everyone.
  - [WSL and WSL2 from Microsoft](https://docs.microsoft.com/en-us/windows/wsl/install-win10)
  - [ESL and WSL2 from OMG Ubuntu](https://www.omgubuntu.co.uk/how-to-install-wsl2-on-windows-10)
  - GUI apps work great when you install [Vcssrv](https://sourceforge.net/projects/vcxsrv/) or [Xming](https://sourceforge.net/projects/xming/)

## Mac OSX
- [Fuzzy and/or jaggedy fonts on external screens](mac/blurry-fonts.md)
