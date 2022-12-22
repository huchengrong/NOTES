# 发送邮件

1. 批量

```bash
swaks --to $(cat emails | tr '\n' ',' | less) --from test@sneakymailer.htb --header "Subject: test" --body "http://10.10.14.29/" --server 10.129.2.28
```

eamils是获取的全部邮箱

1. 单独

```bash
swaks --to eric@madisonhotels.com --from vvaughn@polyfector.edu --server 192.168.149.131:2525 --body "My kid will be a soccer player"  --header "Subject: My kid will be soccer player"
```
