# VNC client and server

<tt>Updated: Wed 29 Jul 15:57:01</tt>

-----------------------------

- This assumes that a VNC client and server have been installed in the host and remote systems. Most of the instructions below are general, but TigerVNC is/was used for both client and server. If you need to install VNC client and/or server, see: [vnc-installation.md]
- The connection method used here is `ssh` tunneling due to its safety. See, for example, [Accessing vncserver via SSH tunnels](https://wiki.archlinux.org/index.php/TigerVNC#Accessing_vncserver_via_SSH_tunnels). 
- It is assumed that the VNC server is not running (automatically started at startup). Here, we access the remote computer and start the service and terminate it at the end.

## Linux: Create an ssh tunnel from your computer to the remote computer 
  - Assuming Linux host and Linux remote computer

**1. On local host: Create a tunnel between the host (your local computer) and remote computer:**
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
 
**2. On remote: Check if a vnc server is already running**
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

**3. On remote: Start vnc server**
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
 
 **4. On local: Start `vncviewer`**
 Giving the command 
  ```
  vncviewer
  ```
  This opens the program and in the box asking for VNC server, you should write
  ```
  localhost:5901
  ```
  If you opened another port instead of 5901, then use that number. Check also the `Options` menu especially for `Input` as you probably want shared clipboard (if there are problems in connecting, you may need to check the `Security` menu.)
  
 **5. On remote: Stopping the vnc server** 
 You can, of course leave the server running, but it is probably a good idea to terminate the process when you are dine with the session. This is done as instructed above, that is:  check the servers that are running and terminate them:
 
 ```
 vncserver -list
 vncserver -kill :*
 ```
   - the wildcard `*` kills all the `vncserver` processes.

With the above, you should be able to establish VNC sessions.
