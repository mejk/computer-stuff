Edit `/etc/default/grub`:
```
sudo vi /etc/default/grub
```
Edit the line that says
```
GRUB_DEFAULT=0
```
For example, editing it to
```
GRUB_DEFAULT="1>2"
```
The first digit means that Grub will pick the second entry from the main menu (shows up as 'Advanced options for Ubuntu' at boot time) and the second digit tells Grub to pick the third entry from the submenu.

After done, run
```
sudo update-grub
```
