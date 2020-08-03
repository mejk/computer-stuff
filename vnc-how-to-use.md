# VNC client and server basic use

<tt>Updated: Sat 1 Aug 09:57:01</tt>

-----------------------------

- This assumes that a VNC client and server have been installed in the host and remote systems. Most of the instructions below are general, but TigerVNC is/was used for both client and server. If you need to install VNC client and/or server, see: [vnc-installation.md]
- The connection method used here is `ssh` tunneling due to its safety. See, for example, [Accessing vncserver via SSH tunnels](https://wiki.archlinux.org/index.php/TigerVNC#Accessing_vncserver_via_SSH_tunnels). 
- It is assumed that the VNC server is not running (automatically started at startup). Here, we access the remote computer and start the service and terminate it at the end.

## 1. Linux client, Linux remote: Create an ssh tunnel from your computer to the remote computer 
  - Assuming Linux host and Linux remote computer

### 1.1 On local host: Create a tunnel between the host (your local computer) and remote computer:
```
ssh -L 5901:localhost:5901 -C -l username_on_remote_computer your_remote_computer
```
For example, assume that we have user `foo` and the remote computer is called `comp1.remote.net`, the the above becomes
```
ssh -L 5901:localhost:5901 -C -l foo `comp1.remote.net`
```
Here's what the above means:

- switches:
  - `-L`: allows specifying ports ont the host (the first number) and remote computer (the second number).
    - `-L 5901:localhost:5901` means allowing for connections between the local computer's port `5901` and remote computer port `5901`. That is, a tunnel is created. 
  - `-C`: compresses data
  - `-l`: username on the remote computer
 
### 1.2. On remote: Check if a vnc server is already running 
Now you should be logged in using the above tunnelling method. Now it is time to start the `vnc` server:
  - Check first that there is no vnc server running:
    ```
    vncserver -list
    ```
   - If there is, you should probably terminate the process. For example, if `vncserver -list` gives you the following output:
     ```
     TigerVNC server sessions:

     X DISPLAY #	RFB PORT #	PROCESS ID
     :1		  5901		    15268
     ```
     Then you can kill it by using the X-Display port number:
     ```
     vncserver -kill :1
     ```
  ## 1.3 On the remote: Create `xstartup` file in `~/.vnc`
   If you went through the server installation instructions, you do, but in case not (server was installed for you), this is what you should do (the script assumes that XFCE4 has been installed): A startup script is needed for the remote desktop configuration. We need to create file `~/.vnc/xstartup`. Use your favourite (ASCII) editor (I am using emacs) and ensure that it is executable (otherwise it won't work):

 ```
  emacs ~/.vnc/xstartup
  chmod a+x xstartup
  ```
  Here is the contents of the xstartup file (there are many other options but this works):
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
  

### 1.4. On remote: Start vnc server
  Now, there should be no server running so we can start new one. Here's how:
  ```
  vncserver -geometry 800x600 -alwaysshared -localhost :1
  ```
   - NOTES:
       - `:1` means: X-Display number 1. If it is taken, change the number. This is also the number that `vncserver -list` shows. 
       - `-geometry` gives the geomoetry of the window to be opened. It can of course be resized (check the options when you use the TigerVNC client)
       - `-localhost`. This means that only local connections are allowed -- this is where tunneling comes to play. 
       - `-alwaysshared`:  allows for shared desktops (not necessary, though)
       - For more options, check tha vncserver man pages.
 
### 1.5. On local: Start `vncviewer`
 Giving the command 
  ```
  vncviewer
  ```
  This opens the program and in the box asking for VNC server, you should write
  ```
  localhost:5901
  ```
  If you opened another port instead of 5901, then use that number. Check also the `Options` menu especially for `Input` as you probably want shared clipboard (if there are problems in connecting, you may need to check the `Security` menu.)
  
 ### 1.6. On remote: Stopping the vnc server  
 You can, of course leave the server running, but it is probably a good idea to terminate the process when you are dine with the session. This is done as instructed above, that is:  check the servers that are running and terminate them:
 
 ```
 vncserver -list
 vncserver -kill :*
 ```
   - the wildcard `*` kills all the `vncserver` processes.

With the above, you should be able to establish VNC sessions from Linux to Linux.

### 1.7 On the remote: Do I have a vnc server running?

It may not be such a bad idea to add the following line at the end of your `.profile` file:
```
vncserver -list
```
This shows you, upon login, if there is a vncserver running.

## 2. Windows client, Linux remote 

### 2.1 Case 1: Using WSL (Windows Subsystem for Linux)

- This assumes that WSL has been installed.
- Steps **1.1 - 1.4** are the same. In this case you just open an Ubuntu shell on Windows go throuhg the steps
- Step **1.6** stopping the `vncserver` is also the same.
- The only difference is installation of TigerVNC. To do that:
  - Go to [TigerVNC Releases](https://github.com/TigerVNC/tigervnc/releases) and get the binary for the latest version. There are binaries for the full TigerVNC client and server and client only. You just need the client. Install. 
  - Start like any other program windows program. The interface is exactly the same for the Linux client, so see the comments in **1.6**.
  
### 2.1 Case 2: Using putty and TigerVNC

- This assumes that putty has been installed
- You need to login to the remote computer and start the server using your `ssh client` (putty in this case). That means executing steps **1.2 - 1.5**
- Create a tunnel using putty. 
  - See these sites for instrcutions:
    - [How to Tunnel VNC over SSH](https://helpdeskgeek.com/how-to/tunnel-vnc-over-ssh/)
    - [VNC over ssh using putty in Windows](https://medium.com/@madhav2code/vnc-over-ssh-using-putty-in-windows-d82ac35dc25e)
- Install TigerVNC as in **2.1 Case 1**. 
- - Step **1.6** stopping the `vncserver` is also the same as above.

## 2. OSX client, Linux remote 

Go to [TigerVNC Releases](https://github.com/TigerVNC/tigervnc/releases) and get the binary for the latest version. The binary inlcues the TigerVNC client. To be able to connect to a Linux host. Simply install it and as with both Linux and Windows, create an ssh tunnel and start the TigerVNC client.  
