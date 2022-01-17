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

If you want to change the timeout style, edit the line `GRUB_TIMEOUT_STYLE`. The options are `menu`, `hidden`, `countdown`. Let's set it to menu:
```
GRUB_TIMEOUT_STYLE=menu
```

Once done, apply the changes by updating Grub using the command
```
sudo update-grub
```
