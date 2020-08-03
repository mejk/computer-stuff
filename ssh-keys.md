# ssh keys, aliases and connecting using ssh keys

_Use at your own risk. Now guarantees of any kind, implied or explicit, are given._

**Never share your private key with anyone**

---

Last updated: Sat 11 Jul 11:40:45 EDT 2020

#### Why: 
ssh keys are needed for safe shell connections between computers over networks. Works on Linux/unix, Windows, Mac. In addition to security, ssh keys provide also lots of other goodies such as keeping the connection alive over extended periods. Some of these matters are discussed below and see also the provided links for more information. 

#### Local note:
All of our group's local computers use ssh keys, so you do need to set them up to connect: no ssh keys, no connection.



------

#### More info regarding ssh keys: 
- [SSH keys from ArchLinux documentation](https://wiki.archlinux.org/index.php/SSH_keys)
- [ssh-keygen from Wikipedia](https://en.wikipedia.org/wiki/Ssh-keygen)
- [How to set up ssh keys on linux/unix from cyberciti](https://www.cyberciti.biz/faq/how-to-set-up-ssh-keys-on-linux-unix/)
- [How to configure ssh key based authentication on a Linux server](https://www.digitalocean.com/community/tutorials/how-to-configure-ssh-key-based-authentication-on-a-linux-server)

-----

## 1. On Linux 
[](#lnx)

The very first thing is to open a terminal. The commands below will be given on the terminal screen.

### 1.1 Generate ssh keys (skip to 1.2 if you have already done this)
If not already in your home directory, go there by giving the command
```
cd
```
Now we are ready to generate ssh keys. Note that there are a lot of options (see for example the above links), but below we only select the number of bits to be 4096 (you can also use the default but dropping out the `-b` option; that will generate 2048 bit keys). To generate (4096 bit) ssh keys, give the command
```
ssh-keygen -b 4096
```
You will then be prompted for the file where to store they keys. Unless there is some particular reason (usually not), simply use the default. That will put the ssh keys in the file `id_rsa.pub` in directory `.ssh` under your home dierctory (that is: `~your_username/.ssh`). To use the default, just press enter:
```
your_username@host:~$ ssh-keygen -b 4096
Generating public/private rsa key pair.
Enter file in which to save the key (/home/your_username/.ssh/id_rsa): 
```
You will then be asked for a passphrase (it is generally a good idea to use one). Note that is password is not the same as your computer password, this is just for ssh keys (if you forget it, it will be impossible to get it back). 
```
Enter passphrase (empty for no passphrase): 
```
If you opted to use a passphrase, you will be prompted to confirm it:
```
Enter same passphrase again: 
```
After that, you will get a confirmation (key fingerprint and randomart image).

### 1.2 Copy the ssh keys to the host
Once done, copy it to the computer to which you want to connect to. In the snippet below, replace `remote_host` by the host name and `username` by your user name on the host computer:
```
ssh-copy-id username@remote_host
```
### 1.3 Test that it works
#### Possible problems:
You may get error message:
```
 Permission denied (publickey).
``` 
This typically means that your system administrator has blocked access to the computer. Check that with your sysadmin.


### 1.4 Make connecting easier: Config file Agents, aliases and such
One very useful feature is the the possibility to use a `config` file (the file should be called `config`). It must be located in your `.ssh` directory. Here is an example of a `config` file, just add your own hosts and change `your_username` to yours. After setting up the config, ssh agent will be set up in the next section to make connecting even easier.
```
#=======================================================================
# Template for config file  (~your_username/.ssh/config)
#-----------------------------------------------------------------------
# The first block provides features for all the hosts (Host *).
# Line: 
#       1) the connection is kept alive for this long,
#       2) allows for agent forwarding, 
#       3)-4): X11 port forwarding
Host *
    ServerAliveInterval 120
    ForwardAgent yes
    ForwardX11 yes
    ForwardX11Trusted yes
#-----------------------------------------------------------------------    
# This block defines the host computers:    
Host hostname_1
    HostName hostname_1.your.domain
    User your_username
# If port number is needed, use:
#    Port port_num
#
# If more hosts as needed, just repeat the relevant parts of the above
Host hostname_2

```

### 1.5 Make connecting easier: ssh agent
After setting up the config file, adding ssh agent makes connecting very convenient. Here is how you start the ssh agent:

```
eval 'ssh-agent'
ssh-add
```
Try connecting and you will notice how seamlessly everything works.

## 2. On OSX

The procedure is the same as for Linux. As abobe, the very first thing is to open a terminal. The commands below will be given on the terminal screen.

**2.1** As in step **1.1**, we generate the keys

```
ssh-keygen -b 4096
```

**2.2** As in step **1.2**, we generate the keys and copy them to the computer to which you want to connect to. In the snippet below, replace `remote_host` by the host name and `username` by your user name on the host computer:
```
ssh-copy-id username@remote_host
```

If there are problems or if you want to set up an `ssh agent`, see the steps **1.3-1.5**
