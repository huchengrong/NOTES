# \*隧道

1. 对目标主机8000打隧道

```bash
./chisel server -p 6666 --reverse
./chisel client 10.10.14.29:6666 R:9999:127.0.0.1:8000
```

1. ssh隧道
2. 对目标主机8000打隧道

```bash
ssh nadine@10.10.10.184 -L 8443:127.0.0.1:8443

应用级
ssh -N -D 192.168.119.194:3333 student@192.168.194.52 -p 2222
192.168.119.188是本机，3333是socks4代理
```

1. windows中端口转发

```bash
服务端
./chisel server -p 8000 --reverse
客户端
./c.exe client 10.10.14.5:8000 R:910:localhost:910
然后即可监听910端口
```

1. windows中socks转发

```bash
1. 建立服务端
./chisel server -p 12345 --reverse
本地开启12345启动服务
2. 建立客户端
chisel.exe client 【kali的ip:port】 R:socks
3. 添加sock（proxychains添加socks5即可）
```
