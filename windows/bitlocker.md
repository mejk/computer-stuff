How to remove bitlocker encryption from Windows 10 (done on Dell XPS 13 9360)

(http://users.isr.ist.utl.pt/~mbayat/hacks/how-to-remove-bitlocker-encryption-in-windows-10/)

Here are the commands copied from the above web site:

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
to see until it is done.

5. Restart the PC.
