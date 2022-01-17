# How to add boot delay

This requires editing the file

```
/etc/default/grub
```
For example,
```
sudo vi /etc/default/grub
```
In that file add the line, or if it exists edit it, 
```
GRUB_TIMEOUT=n
```
and change `n` to the desired value (in seconds).

Once done, apply the changes by updating Grub using the command
```
sudo update-grub
```
