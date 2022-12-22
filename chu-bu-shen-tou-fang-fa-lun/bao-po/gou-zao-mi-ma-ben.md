# 构造密码本

1. 利用john以及cewl抓取的英文字母密码构造成强密码（很多基密码）

```bash
1. 打开jogn规则列表
gedit /etc/john/john.conf

2. 找到关键字，开始添加规则
[List.Rules:Wordlist]
最下面，意味着数字将添加到最后
一个$[0-9]代表一位数

$[0-9]$[0-9]$[0-9]

3. 生成字典
john --wordlist=cewl.txt --rules --stdout > pass.txt
```

1. crunch（随机基密码或者固定基密码）

```bash
例如，这就是生成buddy开头的跟4个数字再跟两个特殊字符
crunch 11 11 -t buddy%%%%^^

详细规则
crunch 4 6 0123456789ABCDEF -o crunch1.txt 
用所给字母生成4-6位
crunch 4 4 -f /usr/share/crunch/charset.lst mixalpha 
使用charset.lst（mixalpha字符集）生成只有4位

@ 小写字母
, 大写字母
% 数字
^ 符号
```

‍
