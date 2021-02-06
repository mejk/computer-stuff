## Based on:
- [Can't get SSH daemon running on macOS](https://unix.stackexchange.com/questions/515894/cant-get-ssh-daemon-running-on-macos)
- [X11 forwarding request failed on channel 0](https://discussions.apple.com/thread/7978992)
- [](https://discussions.apple.com/thread/6825969)

To be able to have an X-connection to Mac, edit the file `/etc/ssh/sshd_config` as root and make the following changes/additions:

```
X11Forwarding yes
XauthLocation /opt/X11/bin/xauth
X11DisplayOffset 10
X11UseLocalhost no
````

```
sudo launchctl unload /System/Library/LaunchDaemons/ssh.plist
sudo launchctl load -w /System/Library/LaunchDaemons/ssh.plist
```
If that gives an error message, try

```
sudo launchctl stop com.openssh.sshd 
sudo launchctl start com.openssh.sshd 
```
Try connecting now with `ssh -X` or `ssh -Y`.
