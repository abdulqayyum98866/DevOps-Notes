# 1 - Install PowerShell using WinGet

Source: https://learn.microsoft.com/en-us/powershell/scripting/install/install-powershell-on-windows?view=powershell-7.5

WinGet, the Windows Package Manager

## 1.2 - Install PowerShell using Microsoft Store
Open it.

## 1.3 - Check version
Type to know powershell version.
```powershell
> $PSVersionTable
```
## 1.4 - Major monor package (Check version details)
```powershell
> $PSVersionTable.psversion
```
## 1.5 - IMPORTANT CLARIFICATION (Very Important)
**Note:** Use PowerShell 7+, not old Windows PowerShell
## 1.6 - Search for the latest version of PowerShell
```powershell
> winget search --id Microsoft.PowerShell
```
## 1.7 - To determine whether PowerShell may be upgraded with WinGet, run the following command
```powershell
> winget list --id Microsoft.PowerShell --upgrade-available
```
## 1.8 - If there is an available upgrade, the output indicates the latest available version. Use the following command to upgrade PowerShell using WinGet
```powershell
> winget upgrade --id Microsoft.PowerShell
```
# 2 - Connect to AWS EC2 instance through powershell using SSH client
Source: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/connect-linux-inst-ssh.html

## - PREREQUISITES (CHECK ONCE)

EC2 Public IP

Key file (.pem)

Username

Ubuntu → ubuntu

Amazon Linux → ec2-user

## 2.1 - Go to Folder Where .pem File Exists
```powershell
PS C:\\> cd E:\\
PS E:\\> pwd

Path
----
E:

PS E:\\> cd .\Keys\
PS E:\\Keys> ls

Directory: E:\Keys

DevOps_ap_tokyo.pem
```
## 2.2 – Fix Permission on .pem File (IMPORTANT)

**Note:** Install an SSH client on your local computer (if needed).

Windows blocks SSH if file permissions are too open.

Run the following commands once:

```powershell
icacls.exe Linux_practice.pem /inheritance:r
icacls.exe Linux_practice.pem /grant:r "$($env:USERNAME):(R)"
```

## 2.3 - To connect to your instance using an SSH client
### (Public DNS) To use the public DNS name, enter the following command.
```powershell
ssh -i /path/key-pair-name.pem instance-user-name@instance-public-dns-name
```
The following is an example response.
---
The authenticity of host 'ec2-198-51-100-1.compute-1.amazonaws.com (198-51-100-1)' can't be established.
ECDSA key fingerprint is l4UB/neBad9tvkgJf1QZWxheQmR59WgrgzEimCG6kZY.
Are you sure you want to continue connecting (yes/no)?

Enter `yes`
---
Warning: Permanently added 'ec2-198-51-100-1.compute-1.amazonaws.com' (ECDSA) to the list of known hosts.

**Note:** The instance is connected.





