# Transferring files between Linux and Android

This can be sometimes troublesome. Some tools that have worked:

## Kdeconnect

Install `kdeconnect` on the mobile device and Linux. This uses wifi (need to be on the same network) to connect the devices and has many more functions that just file transfer.

## gmtp & mtp-tools

Not sure if both are needed, but when both installed file transfer using USB works. 

Note that the Android device should be in *"Use USB to transfer files"* (or photos if that's the need) mode. The device will prompt this when connecting the USB cable.

Simple installation:

```
sudo apt install gmtp mtp-tools
```
