数据库是一个具有客户端，具有服务端的网络程序

安装mysql的时候，我们再安装mysql的client和server

mysqld具有网络功能



进行某种工作——数据管理

sql语句——通过网络方式

musql client给server发送sql语句

可以做的更专业

![image-20220530161709575](C:\Users\imdan\AppData\Roaming\Typora\typora-user-images\image-20220530161709575.png)



```sql
show databases;
create database t1;
use t1;
create table if not exist user(
    name varchar(8),
    age int,
);
```

表：表存数据的普通文件

服务器——mysql程序

数据库——目录

表——普通文件



数据按照一定的缓存策略进行刷新



一行数据  ==  一条记录

DDL

DML

DCL

默认字符集

校验规则

```sql
create database db1 charset=utf8 collate uft8_general_ci;
SHOW DATABASES;
// 显示创建数据库使用的SQL语句
show create database xxx;
ALTER

```

