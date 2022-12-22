# 变种密码爆破

password是已知密码 hash是其变种的hash

```bash
hashcat -m 3200 hash password --user -r /usr/share/hashcat/rules/best64.rule
```
