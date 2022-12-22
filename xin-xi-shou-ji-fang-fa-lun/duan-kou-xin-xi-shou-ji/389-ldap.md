# 389（ldap）

1. 枚举三步走

```bash
也可以nmap扫描一下漏洞，一般没有
nmap --script=ldap* 10.129.95.180
看子域
ldapsearch -h 10.10.10.192 -x -s base namingcontexts
带凭据的信息查询
ldapsearch -h 10.10.10.192 -b "DC=BLACKFIELD,DC=local" -D 'support@blackfield.local' -w '#00^BlackKnight' > 1.txt
拥有一个凭据进一步枚举域用户信息
ldapdomaindump -u 'support\ldap' -p 'nvEfEK16^1aM4$e7AclUf8x$tRWxPWO1%lmz' dc.support.htb

三步走如下：
ldapsearch -H ldap://10.10.10.161:port/ -x -s base '' "(objectClass=*)" "*" +     可以枚举出一些域信息，构成第二部的dc参数
ldapsearch -H ldap://10.10.10.161:port/ -x -b DC=htb,DC=local 
ldapsearch -H ldap://10.10.10.161:port/ -x -b DC=htb,DC=local "(objectClass=person)" |   grep "sAMAccountName:" 
最后一步枚举用户
```
