## 基本用法
```sh
# 1 创建数据库
CREATE DATABASE testdb OWNER dbuser;

# 2 列出所有数据库
\l 

# 3 连接数据库
\c testdb

# 4 创建表和查看表
CREATE TABLE student(id int, name varchar(20), birth_date date);
\d # 查看所有表
\d student # 查看当前表结构
\d+ student # 显示更多的信息，如：与表列关联的注释

# 5 插入数据
INSERT INTO student(id, name, birth_date) values(1, 'a', '2010-10-10');
INSERT INTO student(id, name, birth_date) values(2, 'b', '2010-10-12');

# 6 查询表
SELECT * FROM student;

# 7 修改
UPDATE student SET name='aa' WHERE id = 1;
UPDATE student SET name='bb' WHERE id = 2;

# 8 删除
DELETE FROM student where id = 1;

# 9 删除表
DROP TABLE student;
```

## 安装
```
sudo apt-get install postgresql-client
sudo apt-get install postgresql
```

- [PostgreSQL新手入门](http://www.ruanyifeng.com/blog/2013/12/getting_started_with_postgresql.html)

```sh
\h：查看SQL命令的解释，比如\h select。
\?：查看psql命令列表。
\l：列出所有数据库。
\c [database_name]：连接其他数据库。
\d：列出当前数据库的所有表格。
\d [table_name]：列出某一张表格的结构。
\du：列出所有用户。
\e：打开文本编辑器。
\conninfo：列出当前数据库和连接的信息。
```

## 注意
- 要用`;`来结束语句；
- 字符串要用单引号`'`来包裹；


## enable remote connection
- [Configure PostgreSQL to allow remote connection | BigBinary Blog](https://blog.bigbinary.com/2016/01/23/configure-postgresql-to-allow-remote-connection.html)

sudo service postgresql restart

## 参考资料
- [PostgreSQL 入门 - CSDN博客](https://blog.csdn.net/Chen_Victor/article/details/55515266)
- [PostgreSQL - 随笔分类 - Stephen_Liu - 博客园](https://www.cnblogs.com/stephen-liu74/category/343171.html)
- 《PostgreSQL修炼之道》


## Permission denied for relation

```sql
-- login in admin:
psql -U postgres -d exampledb -h 127.0.0.1 -p 5432;
-- grant 
GRANT ALL PRIVILEGES ON ALL TABLES user_tbl TO dbuser;

-- login in dbuser
psql -U dbuser -d exampledb -h 127.0.0.1 -p 5432;
```

## 命令
https://stackoverflow.com/questions/26277356/how-to-get-current-database-and-user-name-using-a-select-in-postgresql/26277430

查看当前用户；
```sql
select user;
```

查看当前数据库
```sql
select current_database();
```