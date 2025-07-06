
# Boot freezes to `loading ramdisk...`

Answer from [here](https://askubuntu.com/questions/1240152/boot-freezes-and-loading-initial-ramdisk):

In safe-mode or command line, edit /etc/default/grub and replace in the existing configuration line
```
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"
``
with
``
GRUB_CMDLINE_LINUX_DEFAULT="dis_ucode_ldr"
``
the issue is either caused by restarting in a different display configuration that it was prior. Either previously having connected a display and starting without it, or not having and starting with it. It happens when having set up UEFI startup mode, and might be fixed by BIOS update.

The usual way of fixing ramdisk issue here apt update && apt upgrade here did not help, or helped in connection with the mentioned solution.
