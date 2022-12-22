# usb

USB 通常安装在 /media 输入mount查看所有挂载 然后复制到本地关键字搜索media 就可以知道安装在了/media下的哪里

数据恢复

```bash
ssh pi@10.10.10.48 "sudo dd if=/dev/sdb | gzip -1 -" | dd of=usb.gz

这里的/dev/sdb指的是mount查出来的虚拟目录，而不是/media的实际目录

gunzip usb.gz
extundelete usb --restore-all
```
