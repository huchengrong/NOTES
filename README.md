# 端口信息收集

### nmap端口探测

```bash
1. 全自动扫描（可选）
./nmapAutomator.sh --host 192.168.3.151 --type All

2. tcp扫描
nmap -p- --min-rate 10000 -A  10.10.11.145

3. udp扫描
nmap -vvv -sU -o nmapudp 10.129.138.220 --max-retries 0
```

### 其他用途探测

```bash
1. 存活探测
nmap -sP 192.168.247.0/24   
```

