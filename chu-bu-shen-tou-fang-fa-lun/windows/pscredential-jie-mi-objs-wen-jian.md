# PSCredential解密（objs文件）

\<Objs开头的加密文件 需要具有当前用户凭证

```clike
(Import-CliXml -Path root.txt).GetNetworkCredential() | fl
或者
powershell -c "$cred = Import-CliXml -Path cred.xml; $cred.GetNetworkCredential() | Format-List *"
```
