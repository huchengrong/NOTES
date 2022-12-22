# \*检索文件

```python
这个是第一王者
Get-ChildItem -Path C:\ -Filter user.txt -Recurse -ErrorAction SilentlyContinue -Force

dir "\user.txt" /s
dir "\local.txt" /s
where /R c:\ bash.exe

下面这个王中王（）主要用来找关键字好用
for /r c:/ %i in (CloudMe*) do @echo %i
Get-ChildItem c:\  -Include *.txt -recurse -erroraction -force
上面这个也好用
```
