## 表的约束

### 1.空属性

null和not null

```sql
select null;
select 1+null;
```

null不能进行计算、比较4

添加非空约束

```sql
create table if not exists class(
	class_name varchar(20),
	class_room varchar(20)
);
desc class;
select * from class;
drop table class;
create table if not exists class(
	class_name varchar(20) not null,
	class_room varchar(20) not null
);
desc class;
insert into class(class_name, class_room) values('1班', '101教室');
```



### 2.默认值

```sql
create table if not exists t12(
	name varchar(20) not null,
    age tinyint default 18,
    sex char(1) default '男'
)engine=InnoDB default charset=utf8;
desc t12;
insert into t12(name) values('唐三藏');
select * fron t12;
insert into t12(name, sex) values('唐三藏', '女');
select * fron t12;
insert into t12(name, sex, age) values('唐三藏', '女', 99);
select * fron t12;
```

default和not null同时设置可以，但一般不同时出现

### 3.列描述

comment，注释，不影响逻辑

```sql
create table if not exists t13(
	name varchar(20) not null comment '这是用户名',
    age tinyint unsigned default 18 comment '这是用户年龄',
    sex char(1) default '女' comment '这是用户性别'
);
desc t13;
show create table t13 \G
```

### 4.zerofill

整数后面带数字：显示宽度

小于位宽前面补0，大于等于不显示0

```sql
create table if not exists t14(
	a int(10) unsigned default 6,
    b int(10) unsigned default 8
);
alter table t14 change a a int(10) unsigned  zerofill default 6;
desc t14;
insert into t14 values(2,1);
select * from t14;
```

### 5.主键

主键：primary key用来唯一的约束该字段里面的数据，不能重复，不能为空，一张表中最多只能有一个主键；主键所在的列通常是整数类型
如果设置了主键，约束体现在：

1. 任何主键都不能重复，不能为空
2. 一旦插入相同主键的值，MySQL就会出现主键冲突报错，终止运行，意味着只要插入到表中的数据，主键一定是不冲突的

```sql
create table if not exists t16 (
	id int unsigned primary key comment '学号',
    name varchar(20) not null
);
desc t16;
insert into t16(id,name) values(1,'zhangsan');
insert into t16(id,name) values(2,'lisi');
alter table t16 drop primary key;
alter table t16 add primary key(name);
```

### 6.复合主键

在创建表的时候，在所有字段之后，使用primary key(主键字段列表)来创建主键，如果有多个字段作为主键，可以使用复合主键

```sql
create table t17(
    id int unsigned,
    course char(10) comment '课程代号',
	score decimal(4,1) default 60.0 comment '该课程的得分'
);
alter table t17 add primary key(id, course);
insert into t17 values(1, '123', 90.5);
insert into t17 values(1, '124', 90.5);
insert into t17 values(2, '123', 90.5);
```

### 7.自增长

auto_increment：当对应的字段，不给值，会自动的被系统触发，系统会从当前字段中已经有的最大值+1得到一个新的不同的值。通常和主键搭配使用，作为逻辑主键

primary key auto_increment 自增字段，但并不代表你不能自己设置

### 8.唯一键

主键、唯一键都是唯一的，唯一键可以为空

唯一键的约束问题：

其他具有唯一性的数据也要具有唯一性

unique

维护在数据库表内，彼此之间不要冲突

```sql
create table if not exists t19(
	id int unsigned primary key,
    name varchar(20) not null,
    telephone char(32) unique not null
);
```

### 9.外键

```sql
foreign key (xxx) references xxx(xxx)
```

外键用于定义主表和从表之间的关系

表和表本质就是2个独立的文件

当不存在某个班级的时候，在学生表中插入一个不存在班级的学生，不想让他插入成功

```sql
create table if not exists Class(
    class_name varchar(20) primary key
);
create table if not exists Stu(
	id int primary key,
    name varchar(20) not null,
    class_id varchar(20)
);
insert into Class values('100');
insert into Class values('101');
insert into Stu values(1, '张三', '100');
insert into Stu values(2, '李四', '101');
select * from Stu,Class where Stu.class_id=Class.class_name;
create table if not exists Class(
    class_name varchar(20) primary key
);
create table if not exists Stu(
	id int primary key,
    name varchar(20) not null,
    class_id varchar(20),
    foreign key Stu(class_id) references Class(class_name)
);
```

一张表修改影响另一张表，阻止非法操作



