## Some random tips and tricks

### What is my Ubuntu version + other details:
```
uname -m && cat /etc/*release
```
or
```
uname -a
```

### How to see what is your MAC address
The command `ifconfig` has been deprecated some time ago (it can be installed, of course), so it is better to use something else like `ip`:
```
ip addr show
```
or
```
ip a
```
Not exactly the same but this can show it too (+other things. ARP = Address Resolution Protocol). Shows the IPv4 network negighbourhood.
```
arp -a
```
On a Mac `ifconfig` works. On Windows, open command window and type `ipconfig /all`.
### How many processors/cores do I have

```
nproc
```
or
```
lscpu
```

- For more, see: [How to find the number of CPU cores including virtual?](https://askubuntu.com/questions/724228/how-to-find-the-number-of-cpu-cores-including-virtual)

### How to see all the current environment variables
This will show you everything. 
```
env
```

### How to copy full directories with the `dot` files preserve

One way to accomplish that is to use `.` after the source directory, that is,
```
cp -p -r /mysrcdir/. /targetdir
```
The flags:
 - `-p`: preserves info about date (timestamps) and ownership
 - `-r`: copy recursively

### How to manage different versions of compilers and Java
- [How to switch between multiple GCC and G++ compiler versions on Ubuntu 20.04 LTS Focal Fossa](https://linuxconfig.org/how-to-switch-between-multiple-gcc-and-g-compiler-versions-on-ubuntu-20-04-lts-focal-fossa)

The instructions below are from the above link:

Install the `build-essential package`
```
sudo apt install build-essential
```
Install the compilers you want, for example (gcc9 is installed by default):
```
sudo apt -y install gcc-7 g++-7 gcc-8 g++-8 
```
This is the importanyt part: One needs to create list of the compiler alternatives. This is done by running the command 'update-alternatives' separately on each of the compilers including the default one:
```
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-7 7
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-7 7
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-8 8
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-8 8
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-9 9
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-9 9
```
Now, one can use the command 'update-alternatives' to select a compilers (gcc and g++ muct be done separately): 
```
sudo update-alternatives --config gcc
sudo update-alternatives --config g++
```
Finally, check the versions to see that the above worked out:
```
gcc --version
gcc++ --version
```

The same works for java. Install your favourite java environments/Development kits. Then, you can see the version using
```
java -version
```
Use the following command to switch between the different options:
```
sudo update-alternatives --config java
```

- For more on Java, see: [How to install Java on Ubuntu 20.04 LTS Focal Fossa Linux ](https://linuxconfig.org/how-to-install-java-on-ubuntu-20-04-lts-focal-fossa-linux)

### Accessing the bootloader in Ubuntu 20.04 LTS
Accessing the bootloader in the earlier versions was easy from the login screen and that has changed a bit. In Ubuntu 20.04 LTS you can enter the bootloader by
 - Pressing the ESC button when booting. This takes you to the bootloader (to access failsafe mode or change boot parameters)

### Detect your Nvidia / graphics driver:
The command 
```
ubuntu-drivers devices
```
tells what you have available. And
```
nvidia-smi
```
tells which Nvidia driver you are using.



### How to customize the bootloader (Grub)
Only use if you know what you are doing.
- [How to Change Default OS Entry in Ubuntu 20.04 Dual-Boot](http://ubuntuhandbook.org/index.php/2020/04/default-os-entry-ubuntu-20-04-dual-boot/)
  - In brief install Grub Customizer: `sudo apt install grub-customizer`
- [How to Update Grub on Ubuntu and Other Linux Distributions](https://itsfoss.com/update-grub/)  
- [Get grub menu back after installing Ubuntu 20.04 alongside Windows](https://medium.com/@leijerry888/get-grub-menu-back-after-installing-ubuntu-20-04-alongside-windows-dab5de5afc37)  

### Getting the `System program problem detected` message upon login?

It is probably the same stuff that keeps on repeating. The error messages are in '/var/crash`. See what ist there:
```
cd /var/crash
ls -lt
```
If the messages are old (see the dates), just remove the files.

### How to make a laptop rebootable (from a remote) with lid closed / How to ignore the lid switch

- The answer below is from here: [Ubuntu goes suspended after login if lid is closed](https://askubuntu.com/questions/1083720/ubuntu-goes-suspended-after-login-if-lid-is-closed)
- Tested on Ubuntu 20.04 LTS

Edit the file (using sudo)
```/etc/systemd/logind.conf```
and then change the line
```
#HandleLidSwitch=suspend
```
to
```
HandleLidSwitch=ignore
```
Save and reboot. If you reboot from a remote you can see if it works.

### Add an SSD or HD and have it automounted

- It's simple. Here are the instructions: [How To Automount File Systems on Linux](https://www.linuxbabe.com/desktop-linux/how-to-automount-file-systems-on-linux)
