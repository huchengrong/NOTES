# 21(ftp)

```bash
1. 普通登陆格式
ftp [ip] [port]

2. 异常处理
epsv4 off
或者
passive

3. 注意事项
注意ftp所在目录是否是web目录

4. 爆破实例
hydra -l rongsec -P rong.txt ftp://127.0.0.1
```
