---
title: PHP中操作数据库
date: 2018-4-19 00:22:31
categories: 
    - 'PHP'
    - 'sql'
tags: 
    - 'sql'
---

# PHP中数据库的增删改查

```sql
查询：
    select * from mytable(默认无序)
    select * from mytable where id = 2
    select * from mytable order by age desc（降序）
    select * from mytable limit4, 10(分页)
    select count(*) from mytable;（）分页的时候用的上
    多表联合查询
        用的最多的left join左边当主表， 右边当副表（连接id查询）
        select * from 左表 left join 右表 on 左表.cid = 右表.id;
增加：
	insert into mytable values(null, ....)
	insert into mytable(字段1名， 字段2....)values(值....)
删除：
	delete from mytable where id = ?
修改：
	update mytable set age = 20, name = 'zs' where id = 2;
```



