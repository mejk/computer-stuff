
# How to extract the 10 Windows 10 licence key 

If Windows 10 is (pre-)installed, then you have already paid for the Windows 10 licence. It is a very good idea to get the Windows OEM product 
key from your computer in case something goes wrong and you need to reinstall or you wish to wipe out Windows and install it in VirtualBox. 

Sometimes the product key is listed in Bios or listed in Windows' settings, but that is often not the case. The key can, however, be extracted from Windows. Here is how to do it.

- More info:
 - [How to Find Your Windows 10 Product Key Using the Command Prompt](https://www.howtogeek.com/660517/how-to-find-your-windows-10-product-key-using-the-command-prompt/)
 - [How to Find Windows Product Key via Command in Windows or Linux](https://osxdaily.com/2018/09/09/how-find-windows-product-key/)

## 1. Within Windows using two possible methods
 - (tried on MSI, Samsung, Dell XPS) 

**Option 1:**
 Open the Windows command window in administrator mode and give the command

```
wmic path softwarelicensingservice get OA3xOriginalProductKey
```
**Option 2:**
 or alternatively, use the Windows PowerShell in administrator mode and give the command:

```
powershell “(Get-WmiObject -query ‘select * from SoftwareLicensingService’).OA3xOriginalProductKey”
```
Now you should have the product key. Save it.

## 2. How to extract Windows 10 licence key within Linux

- Below are two possible methods. This has been tried on MSI, Samsung, Dell XPS using Ubuntu 18.04, 20.04. 

Open a terminal windows and give one of the two commands:

**Option 1:**
```
sudo strings /sys/firmware/acpi/tables/MSDM
```

**Option 2:**

```
sudo cat /sys/firmware/acpi/tables/MSDM

```

## 3. How to extract Windows 10 licence key within VirtualBox running in Linux

- In this case it is (obviously) assumed that you have already installed Windows 10 in a Virtual Box in Linux.

```
cat "~/VirtualBox VMs/win10/msdm.bin"
```
