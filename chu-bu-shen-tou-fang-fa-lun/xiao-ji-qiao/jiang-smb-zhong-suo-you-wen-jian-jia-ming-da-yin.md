# 将smb中所有文件夹名打印

```bash
1. 挂在
mount -t cifs //10.10.10.192/profiles$ /mnt
2. 输出
mv users users.old; ls -1 /mnt/ > users
-1是每行只打印一个
```
