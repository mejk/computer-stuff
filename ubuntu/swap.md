# kswapd0 takes 100% of CPU

Instructions are here: [How To resolve High CPU occupation from kswapd0
Why?](http://kb.lc/01.how_to/kswapd0/)

Summary: 

1. Check swapiness

```
cat /proc/sys/vm/swappiness
```

The default is 60. 

2. Check cache pressure:

```
cat /proc/sys/vm/vfs_cache_pressure
```
The default is 100.

3. Check transparent_hugapage
```
cat /sys/kernel/mm/transparent_hugepage/enabled
```
It should be set to always.

4. The fix: Set swapiness to zero
```
sudo echo vm.swappiness=0 | sudo tee -a /etc/sysctl.conf
```

##  If there is no swap, this may help

- See: [How to Add Swap Space on Ubuntu 18.04](https://linuxize.com/post/how-to-add-swap-space-on-ubuntu-18-04/)

1. Check the swap size:

```
cat /proc/swaps 
```
If it shows nothing, then no swap has been set up. Check also `/etc/fstab` just in case
```
cat /etc/fstab 
```
Check also the filesystem to see if there is a swap allocation
```
df -h -T
```
If no swap has been allocated and set up, set up swapfile

2. Let's set a `swapfile` of 1G, change the rights, set upo swap area and activate it:
```
sudo fallocate -l 1G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
```

3. Add it in `/etc/fstab` by putting the following line in there

```
/swapfile swap swap defaults 0 0
```

4. Check that the swap is on
```
sudo swapon --show
```
