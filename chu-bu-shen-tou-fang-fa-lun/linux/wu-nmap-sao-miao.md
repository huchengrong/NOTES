# 无nmap扫描

```bash
for i in {1..255}; do (ping -c 1 192.168.1.${i} | grep "bytes from" | grep "10.11.1" |  awk '{print $4}' | sed 's/.$//' &); done
for i in {1..65535}; do (echo > /dev/tcp/192.168.1.1/$i) >/dev/null 2>&1 && echo $i is open; done
```
