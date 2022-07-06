```sql
create table info(
	id int primary key auto_increment,
    birthday date
);
insert into info(birthday) values('1980-01-01');
insert into info(birthday) values(current_time());
select * from info;
alter table info add nickname varchar(20) after id;
select * from msg where date_add(sendtime, interval 2 minute) > now();
select ceiling();
select floor();
```

# 复合查询	

select 由内向外	

format放在最后需要显示的时候统一使用



## 多表查询

```sql
select * from deptno;
```

做完笛卡尔积，本质是我们把所有相关的数据，聚合到了一张表，所有的MySQL查询，都变成了对于一张表的查询

我又是如何得知，需要哪些表呢？根据题面追溯需要的数据都在哪些表里面+关联字段

## 自连接

自己和自己做笛卡尔积

