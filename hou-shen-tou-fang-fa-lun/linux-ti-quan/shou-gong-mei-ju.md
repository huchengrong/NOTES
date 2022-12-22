# 😇 手工枚举

```bash
内核、系统信息查询
uname -a    打印所有可用的系统信息
uname -r    内核版本
uname -n    系统主机名。
uname -m    查看系统内核架构（64位/32位）
hostname    系统主机名
cat /proc/version    内核信息
cat /etc/*-release   分发信息
cat /etc/issue       分发信息
cat /proc/cpuinfo    CPU信息
cat /etc/lsb-release # Debian 
cat /etc/redhat-release # Redhat
ls /boot | grep vmlinuz-

可提权SUID查询；(这个是重中之重，后面附加的ls可以更快的识别到我们可以玩的二进制文件)
find / -user root -perm -4000 2>/dev/null -ls
ps aux | grep -v root

查找有权限执行的文件
find / -user student 2>&1 | grep -v "Permission denied\|proc"

注意看用户目录下的 .bash_history
如果不是0字节，就打开看看

查找可读可写可执行的文件（通常用来寻找计划任务）
find / -perm 777 -type f 2>/dev/null
grep "CRON" /var/log/cron.log  找计划任务
或者
for i in `ls /etc/cron.d` ; do cat /etc/cron.d/$i |grep -v "#" ; done


apache如果可能需要www权限，记得去var枚举枚举
```

‍
