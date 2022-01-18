# Synaptic not opening

When running
```
sudo synaptic
```
there's an error message
```
    You are using Wayland environment, Synaptic will continue without administrative privileges.
    To make Synaptic fully functional, please restart your session without Wayland.
```
but Wayland is not running - check using
```
echo $XDG_SESSION_TYPE
```

Solution: Give GUI applications root rights (and then revoke afterwards)
```
xhost +si:localuser:root
```
Now, 
```
sudo synaptic 
```
should work. When done,
```
xhost -si:localuser:root
```
