# VNC client and server installation

**We are using Tigervnc**. It is fast and works with Linux, Windows and Mac.

<tt>Updated: Mon 27 Jul 20:40:06</TT>

Use this instructions at your own risk. No warranties, explicit or implied, are given.

Tested:
 - Ubuntu 20.04 LTS (client and server)
 - Ubuntu 18.04 LTS (client)
 - Ubuntu 16.04 LTS (client and server)


--------

## 0. Before you start: CHECK IF `vncviewer` and/or `vncserver` have already been installed!

## 1a. Install vnc client using package manager: TigerVNC in Ubuntu 20.04 

On Ubuntu 20.04 LTS, the package manager includes the latest version. Install it and the xorg extension for being able to connect to the local desktop directly:
```
sudo apt install tigervnc-viewer
sudo apt install tigervnc-xorg-extension
```
Now you can start the VNC viewer with the command
  ```
 vncviewer
 ```

## 1b. Alternative to 1a: Install vnc client (and server) manually. This works also on Ubuntu 18.04/16.04.
 - Note 1: The version of TigerVNC provided by the package manager on  Ubuntu 18.04/16.0 is an old one so installation using this way gives the latest one.

 - Note 2: The latest version is available from [The latest TigerVNC releases](https://github.com/TigerVNC/tigervnc/releases). The latest at the time of writing this is `1.10.1`. Change the package name below accordingly if necessary.

- Note 3: This procedure installs also the Tigervnc server (there is an option to download the client only if you so prefer).

  1. Download TigerVNC from [The latest TigerVNC releases](https://github.com/TigerVNC/tigervnc/releases). Both binaries and source code are available. This also installs the necessary packages for VNC server.

  2. Extract the package (assuming `~/Downloads` as the download directory)
  ```
  cd ~/Downloads
  tar xzf tigervnc-1.10.1.x86_64.tar.gz
  cd tigervnc-1.10.1.x86_64
  ```
  3. If you execute `ls -l`, you notice that the director inside `tigervnc-1.10.1.x86_64` is called `usr`. This name may be a bit inconvenient so we change it below to reflect the name and version of TigerVNC we are using. We also copy it to `/opt` for transparency (it can also be copied somewhere else if you so prefer). Since we use `/opt`,  we change the owner to root. Here are the commands:
  ```
  sudo chown -R root:root usr
  sudo mv usr tigervnc-1.10.1
  sudo cp -p -r tigervnc-1.10.1 /opt
  ```
  - NOTE: If this is a private installation without `root` rights, you can leave the directory in its place or move somewhere in your own directory system and simply put it in the path following the instructions in the next step (just change the path to TigerVNC accordingly).

  4. To be able to use `vncviewer`, we must put it in path:
  ```
  export PATH=/opt/tigervnc-1.10.1/bin${PATH:+:${PATH}}
  ```
  - IMPORTANT: If you want to make this permanent, edit your `.profile` file and add the above at the bottom of it. Otherwise you have to execute this command every time.

 5. Now you can start the VNC viewer with the command
  ```
 vncviewer
 ```

## 2. Server installation: TigerVNC

More information & the sources that were used:
- [Ubuntu 20.04 Remote Desktop Access with VNC](https://www.answertopia.com/ubuntu/ubuntu-remote-desktop-access-with-vnc/)
- [Install VNC Server with Gnome display on Ubuntu 18.04](https://www.teknotut.com/en/install-vnc-server-with-gnome-display-on-ubuntu-18-04/)
- [Arc Linux TigerVNC](https://wiki.archlinux.org/index.php/TigerVNC)
  - This is an excellent source for lots of info.
  
## 2a. On Ubuntu 16.04/18.04 (or others) and works also on 20.04**

The procedure above in **1b** installed also the server for TigerVNC. Skip to part **2.1. Configuring the server**

## 2b. On Ubuntu 20.04 LTS using the package manager
Very simple: 
 ```
 sudo apt install tigervnc-standalone-server
 ```

### 2.1. Configure the server

1. We want a lightwight desktop environment. The choice here is `XFCE4` simply because the server setup is straightforward and it works very well (and is lightweight). If you already have `XFCE4`, skip to the next step. If you don't have `XFCE4` installed, a minimal installation (=without the XFCE4 default software etc.; you can always add them later very easily) can be done very easily using the package manager:
  ```
  sudo apt install xfce4
  ```

2. Create a password on the vnc server: 
  - IMPORTANT: *This is a password for the being able to access the VNC server, this is NOT the same as your password to access the system.*
   ```
   vncpasswd
   ```
3. A startup script is needed for the remote desktop configuration. We need to create file `~/.vnc/xstartup`. Use your favourite (ASCII) editor (I am using emacs) and ensure that it is executable (otherwise it won't work):
```
emacs ~/.vnc/xstartup
chmod a+x xstartup
```
Here is the contents of the `xstartup` file (there are many other options but this works):
```
#!/bin/sh
unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS
export XKL_XMODMAP_DISABLE=1
##-------------------------------
## SELECT YOUR ENVIRONMENT (here, default is Budgie).
## COMMENT/UNCOMMENT AS NECESSARY
#
# 1. Budgie: Doesn't work properly, don't use. 
#            This is kept for possible future updates
#xhost local:
#gnome-session --session=budgie-desktop &
#budgie-wm &
#budgie-panel &

# 2. XFCE4. 
# Works well.
# If problems occur: 
#  - Check that xstartup is executable and that .Xresources and .Xauthority exist
xhost local:
vncconfig -nowin &
xrdb $HOME/.Xresources
exec startxfce4 
```

4. Check that the files (in your home directory) `.Xauthority` and `.Xresources` exist. If not, create them, e.g., `touch .Xresources`

5. Start the server to try it out:
```
vncserver :1
```
6. Stop the server
```
vncserver -kill:1
```


## Optional (not for normal user): Make VNC server a service.

*Only do this if you know what you are doing.*

To do this, we need to create a new file called `vncserver@.service` and put it in `/etc/systemd/system`. 

- IMPORTANT 1: This is in single user mode. The line `User` has the username of the user of this computer -> replace `foo` by the username. There is also a multiuser mode (see the Arch Linux page).
- IMPORTANT 2: Check that the path to `vncserver` is correct for your system (this one works when TigerVNC is installed using the package manager).

```
sudo emacs /etc/systemd/system/vncserver@.service
```
File contents, replace the username as necessary:
```
[Unit]
Description=Remote desktop service (VNC)
After=syslog.target network.target

[Service]
Type=forking
User=foo
WorkingDirectory=/home/foo

ExecStartPre=/usr/bin/vncserver -kill :%i > /dev/null 2>&1 || : 
#ExecStartPre=/bin/sh -c '/usr/bin/vncserver -kill %i > /dev/null 2>&1 || :'
#ExecStart=/usr/bin/vncserver %i -geometry 1440x900 -alwaysshared
ExecStart=/usr/bin/vncserver - geometry 800x600 -depth 24 -localhost no :%i 
ExecStop=/usr/bin/vncserver -kill %i

[Install]
WantedBy=multi-user.target
```

7. This is how to enable the service automatically at startup
```
sudo systemctl enable vncserver@1
sudo systemctl start vncserver@1

```
8. How to stop the service:
```
sudo systemctl stop vncserver@1
```

