```sql
show databases;
create table if not exists t1(id tinyint);
show tables;
desc t1;
insert into t1 values(1)
select * from t1;

```

为什么MySQL不让插入超范围的数字呢？

答：MySQL是一个专门用来进行数据管理的软件，做到非常严谨，保证MySQL内的数据具有非常强的确定性和一致性，倒逼使用者严格按照MySQL的要求进行数据表中类型的数据与使用。类型本质上是一种约束

```sql
create table if not exists t2 (id tinyint unsigned);
desc t2;
insert into t2 values (1);
create table if not exists t3(a int, b bit(8));
desc t3;
insert into t3(a, b) values (10, 10);
select * from t3;
insert into t3 (a, b) values(97, 97);
select * from t3;
create table if not exists t4(gender bit(1));
insert into t4 values(0);
insert into t4 values(1);
select * from t4;
select hex(gender) from t4;
alter table t4 modify gender bool;
alter table t4 modify gender smallint;
```



常见的取整方案：

 

decimal比float精度高

MySQL char单位不是字节，而是表示字符，表示英文、中文、数字的个数，但是需要1-3个字节来记录数据的大小

```sql
create table if not exists t9(name char(0));
insert into t9 values('a');
select * from  t9;
alert table t9 modify name char(1);
drop table t9;
create table if not exists t9(id int, name char(2));
desc t9;
insert into table t9 vlaues(1, 'a');
insert into table t9 vlaues(1, 'ab');
insert into table t9 vlaues(1, '');
insert into table t9 vlaues(1, 'abc');
insert into table t9 vlaues(1, '哈哈');
insert into table t9 vlaues(1, '哈哈哈');
```

可变长度字符串varchar

关于varchar的len到底是多少，和编码有关；所谓变长就是需要更多的数据来记录长度

变长字符串可以按需给予内存

```sql
create table if not exists t10(id int, name varchar(6));
insert into t10 values (1, 'hello1')
insert into t10 values (1, 'hello11')
create table if not exists t11(id int, name varchar(21844));
```

日期

date：三字节，xxxx-xx-xx

datetime

timestamp

```sql
create table birthday(
	t1 date,
	t2 datetime,
	t3 timestamp
);
insert into birthday (t1, t2) values('1997-01-01', '1998-10-20 12:1:1');
select * from birthday;
insert into birthday (t1, t2) values('2001-01-01',  now());
update birthday set t1='2022-01-01';
```



枚举和集合

enum: 单选类型

set: 多选类型

凡是不在enum或者set中的选项，MySQL都会报错，约束用户的输入，增加MySQL内部数据的确定性或者一致性

```sql
create table votes (
	name varchar(16),
    sex enum('男', '女')，
    hobby set('登山', '编码', '游泳', '武术	')
);
```

find_in_set函数查找集合



为什么MySQL要有数据类型

1.因为MySQL将来第一件事是要建表，所谓的表，本质事一种或多种数据的集合（MySQL中的表，类似C++的class、struct，来描述被管理的对象，本质时描述对象的属性，进行数据化）

2.数据类型本质是一种约束，因为强约束的存在，会保证MySQL中的数据将来会具有很强的一致性和确定性，不会因为上层数据的改变，而影响表中的数据