# 79（finger）

1. 爆破枚举

```bash
枚举脚本如下
pentestmonkey.net/tools/finger-user-enum/finger-user-enum-1.0.tar.gz
枚举方式如下
./finger-user-enum.pl -U /usr/share/seclists/Usernames/Names/names.txt -t 10.129.16.126
得到的结果或许可以用来登陆ssh
```
