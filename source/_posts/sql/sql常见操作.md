---
title: sql常见操作
date: 2016/10/9 20:29
toc: true
comments: true
tags:
- sql
---


获取最大值/最小值
```sql
# 最小值
select min(column_name) from table_name;
select num from table_name order by num;

# 最大值
select max(column_name) from table_name;
select num from table_name order by num desc;

# 获取最大值所在行
SELECT * 
FROM orders
WHERE final_amount = (SELECT MAX(final_amount)
					   FROM orders);
```


参考资料
=======
- [sql中max()和min()取最大值和最小值语句](http://www.111cn.net/database/mssqlserver/42437.htm)

