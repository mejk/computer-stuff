# OpenSSH in Windows 10

**More**: 
 - [Installation of OpenSSH For Windows Server 2019 and Windows 10](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse)
 - [Installing SFTP/SSH Server on Windows using OpenSSH](https://winscp.net/eng/docs/guide_windows_openssh_server) 
 
 Here are the steps to check:
 
 Go to: 
  ```Settings -> Apps -> Apps and Features -> Optional features```
  
  Scroll down if you have `OpenSSH client` and `OpenSSH server` already installed.
  
  If yes, than that is it but if not, then click `Add a feature`
  and scroll down the list to find `OpenSSH client` or/and `OpenSSH server`, and click to install
  
  ## Starting and configuring `ssh server`
  
  Open `PowerShell` as an adminstrator abd give the following commands:
  ```
  Start-Service sshd
  Set-Service -Name sshd -StratupType 'Automatic'
  Get-NetFirewallRule -Name *ssh*
  New-NetFirewallRule -Name sshd -DisplayName 'OpenSSH Server (sshd)' -Enabled True -Direction Inbound -Protocol TCP -Action Allow -LocalPort 22
  ```
