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
This could say:
```
Sourcing file `/etc/default/grub'
Sourcing file `/etc/default/grub.d/init-select.cfg'
Generating grub configuration file ...
Found linux image: /boot/vmlinuz-5.13.0-25-generic
Found initrd image: /boot/initrd.img-5.13.0-25-generic
Found linux image: /boot/vmlinuz-5.11.0-46-generic
Found initrd image: /boot/initrd.img-5.11.0-46-generic
Found linux image: /boot/vmlinuz-5.11.0-27-generic
Found initrd image: /boot/initrd.img-5.11.0-27-generic
Adding boot menu entry for UEFI Firmware Settings
done
```
