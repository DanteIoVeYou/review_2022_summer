插入查询结果（把一张表的选择结果插入另一张表）

```sql
insert into table_name [column] select ...

create table duplicate_table (
	id int,
    name varchar(20)
) engine=InnoDB charset=utf8;
desc duplicate_table;
select * from duplicate_table;
insert into duplicate_table(id, name) values
	(100, 'aaa'),
	(100, 'aaa'),
	(200, 'bbb'),
	(200, 'bbb'),
	(200, 'bbb'),
	(300, 'ccc');
-- #创建一张空表 no_duplicate_table，结构和 duplicate_table 一样
create no_duplicate_table like duplicate_table; 
insert into no_duplicate_table select distinct * from duplicate_table;
```

