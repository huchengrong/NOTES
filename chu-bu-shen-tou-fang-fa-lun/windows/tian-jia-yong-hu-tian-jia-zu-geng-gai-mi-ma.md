# 添加用户，添加组，更改密码

1. 其他组也一样

```clike
1. 创建一个用户
net user fakeadmin passw0rd! /add
2. 加入admin组
net localgroup administrators /add fakeadmin
3. 检查
net localgroup administrators
```

1. 举个例子，利用权限问题，将zensvc用户添加到域用户组并赋予密码以及rdp组

```
net user /domain zensvc xxxxxx
net localgroup "Remote Desktop Users" zensvc /add

```



