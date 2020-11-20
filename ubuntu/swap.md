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

4. The fox: Set swapiness to zero
```
sudo echo vm.swappiness=0 | sudo tee -a /etc/sysctl.conf
```


