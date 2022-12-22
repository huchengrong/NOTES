# 162&162（snmp）

1. 通常操作

```bash
1. 枚举字符串（public等）
onesixtyone 10.10.10.20 -c /usr/share/doc/onesixtyone/dict.txt  

2. 枚举整个min树（常用，下面的几个枚举可能不太需要用）
161/udp open  snmp    SNMPv1 server (public)‘
命令示例；snmpwalk -c public -v1 -t 10 10.11.1.14

3. 枚举用户
snmpwalk -c public -v1 10.11.1.14 1.3.6.1.4.1.77.1.2.25

4. 枚举进程
snmpwalk -c public -v1 10.11.1.73 1.3.6.1.2.1.25.4.2.1.2

5. 枚举开放端口
snmpwalk -c public -v1 10.11.1.14 1.3.6.1.2.1.6.13.1.3

6. 枚举安装的软件
snmpwalk -c public -v1 10.11.1.50 1.3.6.1.2.1.25.6.3.1.2
```

1. 从snmp执行高权限进程

```bash
snmpwalk -v 1 -c public 10.129.228.106 iso.3.6.1.4.1.8072.1.3.2

iso.3.6.1.4.1.8072.1.3.2
来自于snmp枚举到的就选这么多位即可
```
