
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
- 要用`;`来结束语句。


## enable remote connection
- [Configure PostgreSQL to allow remote connection | BigBinary Blog](https://blog.bigbinary.com/2016/01/23/configure-postgresql-to-allow-remote-connection.html)

sudo service postgresql restart

## 参考资料
- [PostgreSQL 入门 - CSDN博客](https://blog.csdn.net/Chen_Victor/article/details/55515266)
- [PostgreSQL - 随笔分类 - Stephen_Liu - 博客园](https://www.cnblogs.com/stephen-liu74/category/343171.html)


## Permission denied for relation

```sql
-- login in admin:
psql -U postgres -d exampledb -h 127.0.0.1 -p 5432;
-- grant 
GRANT ALL PRIVILEGES ON ALL TABLES user_tbl TO dbuser;

-- login in dbuser
psql -U dbuser -d exampledb -h 127.0.0.1 -p 5432;
```