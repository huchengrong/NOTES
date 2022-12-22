# （存在问题）500 (ISAKMP)

1. 通常操作

```bash
ike-scan 10.129.138.220 -M    --探寻属性
/etc/ipsec.conf和 /etc/ipsec.secrets   ---修改配置

修改完了连接即可
ipsec restart 
ipsec up conceal 
```

<figure><img src="https://img-blog.csdnimg.cn/2e76582288ad4bf6885c7e1c1412eaa0.png" alt=""><figcaption></figcaption></figure>

会得到这样的

修改两个文件参数

```bash
/etc/ipsec.secrets
----------------------------------
%any : PSK "Dudecake1!"
----------------------------------

/etc/ipsec.conf
----------------------------------
config setup
    charondebug="all"
    uniqueids=yes
    strictcrlpolicy=no

conn conceal
    authby=secret
    auto=add
    ike=3des-sha1-modp1024!  //修改这里
    esp=3des-sha1!
    type=transport
    keyexchange=ikev1
    left=10.10.14.15   //修改这里
    right=10.10.10.116   //修改这里
    rightsubnet=10.10.10.116[tcp]   //修改这里
-----------------------------------
```
