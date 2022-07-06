主键选择：建议创建与业务无关的键值

# Create

```sql
replace into
```

# Retrieve

查找

全列查询

```sql
select * from exam_result;
```

指定列查询

```sql
select chinese from exam_result;
select chinese,math from exam_result;
select chinese, chinese+10 from exam_result;
select chinese+math+english from exam_result limit 3;
select chinese+math+english from exam_result desc limit 3;
select distinct math form exax_result;
```

条件筛选

```sql
select name, math from exam_result where math > 80;
select name, math from exam_result where math = 80;
```

模糊匹配

like

%

_

select * from exam_result limit 0,2;



# update

```sql
update exam_result set math=80 where name='孙悟空';
update exam_result set math=80;
update exam_result set math=80,chinese=90 where name='孙悟空';
```

# delete

delete from table1;

自增会保存



truncate table1;只能对整个表操作，不能对部分删除



# 插入查询的结果

```sql
```

