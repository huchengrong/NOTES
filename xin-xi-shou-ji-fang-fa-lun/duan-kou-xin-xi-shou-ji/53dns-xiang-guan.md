# 53（dns相关）

1. 挖掘

```bash
dig axfr cronos.htb @10.129.227.211
然后获得新的hosts添加之后继续重复
```

1. dns爆破

```bash
wfuzz -c -w /usr/share/seclists/Discovery/DNS/bitquark-subdomains-top100000.txt -u http://10.10.10.203 -H 'Host: FUZZ.worker.htb' --hh 703
或者
dnsenum --dnsserver 10.129.95.154 -f /usr/share/seclists/Discovery/DNS/bitquark-subdomains-top100000.txt 
```
