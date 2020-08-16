# How to remove bitlocker encryption from Windows 10

---------------------------------

**What is bitlocker**

See:
  - (BitLocker from Wikipedia)[https://en.wikipedia.org/wiki/BitLocker]

Essentially it is a disk encryption method that is set on in many of the new computers.

**Why would you like to remove it?**

- If you plan to use Windows only, there is no real need. However, if you plan to install dual boot it can be quite a pain.

- It may work even with dual boot, see How to install Ubuntu alongside BitLocker encrypted Windows 10 and How To Mount BitLocker-Encrypted Windows Partitions On Linux.
- However, I have had lots of bad experiences especially with computer that have been used for some time before decideing on dual boot. The practical problem is that one needs to partition the SSD/hard drive, it may be really hard to get a large enough a partition for Linux as the SSD/HD gets fragmented. This is why I have typically ended up removing BitLocker.

- Here is the source for the information below:
    - [How to remove BitLocker in Windows 10](http://users.isr.ist.utl.pt/~mbayat/hacks/how-to-remove-bitlocker-encryption-in-windows-10/)


## Let's remove BitLocker:

1. Open the power shell as administrator, by right clicking on it and choosing “Run as Administrator”.
Check the encryption status of each drive by entering:
```
    manage-bde -status
```
2. To disable bitlocker enter (note to put quotations too):
```
    Disable-BitLocker -MountPoint "<drive letter>:"
```
For example:
```
    Disable-BitLocker -MountPoint "C:"
```
3. To remove encryption of the desired drive enter:
```
    manage-bde -off <drive letter>:
```
For example:
```
    manage-bde -off C:
```
4. Let the decryption continue in the background such that you have fully decrypted status. You may check the status of Encryption while it is running in the background. 
Important: Keep checking using 
```
    manage-bde -status 
```
to see until it is done, status `Fully Decrypted`.

5. Restart the PC.

