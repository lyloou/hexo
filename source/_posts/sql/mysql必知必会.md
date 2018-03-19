---
title: mysql必知必会
date: 2018/03/16 20:29
toc: true
comments: true
tags:
- sql
- mysql
---

## 表结构和数据文件 
http://forta.com/books/0672327120/

SQL 是不区分大小写的。
SQL 语句以`;`结束。
SQL 语句中的空格会被忽略，将 SQL 语句分成多行更容易阅读和调试；

## 客户机-服务器软件
- 服务器部分是负责所有数据访问和处理的一个软件。
- 客户机是与用户打交道的软件。
例如，如果你请求一个按字母顺序列出的产品表，则客户机软件通过网络提交该请求给服务器软件。
服务器软件处理这个请求，根据需要过滤、丢弃和排序数据；然后把结果送回到你的客户机软件。
* 服务器软件为MySQL DBMS。
* 客户机软件可以是MySQL提供的工具、脚本语言（如Perl）、Web应用开发语言（如ASP、ColdFusion、JSP和PHP）、
    程序设计语言（如C、C++、Java）等。

## SHOW
```sh
SHOW DATABASE;
SHOW TABLES;
SHOW COLUMNS FROM customers;
SHOW CREATE DATABASE crashcouse;
SHOW CREATE TABLE customers;
```

## 检索
```sql
SELECT prod_name FROM products;
SELECT prod_name, prod_price FROM products; # 检索多列
SELECT * FROM products;  # 除非确实需要表中的每个列，否则最好不要使用`*`通配符，检索不需要的列通常会降低检索和应用程序的性能。
```

### DISTINCT
```sql
SELECT DISTINCT vend_id FROM products;  # DISTINCT 表示只返回唯一不同的行，用法是直接放在列名前，注意不能使用DISTINCT
                                        # DISTINCT 应用于所有列而不是前置它的列。
                                        # 可以通过 LEFT JOIN + IN 的方式：
```

### LIMIT
```sql
SELECT prod_name FROM products LIMIT 5;     # 返回前5行；类似 LIMIT 0,5
SELECT prod_name FROM products LIMIT 5, 10; # 返回从第5行（包括5）开始的10条数据； 注意下标从0开始。
SELECT prod_name FROM products LIMIT 10 OFFSET 5; # 返回从第5行开始的10行
```

### ORDER BY
关系数据设计理论认为，如果不明确规定排序，则不应该假定检索出的数据的顺序有意义。
```sql
SELECT prod_name FROM products ORDER BY prod_name; 
SELECT prod_name FROM products ORDER BY prod_price;  # 可以用非检索的列来排序 
SELECT prod_name, prod_price FROM products ORDER BY prod_price,prod_name;  # 多列检索 
SELECT prod_name, prod_price FROM products ORDER BY prod_price,prod_name DESC;  # 反序 （默认是ASC——升序）
SELECT prod_name, prod_price FROM products ORDER BY prod_price DESC,prod_name;  # 注意和上面的区别；  
SELECT prod_name, prod_price FROM products ORDER BY prod_price DESC,prod_name DESC;  # DESC 关键字只应用到直接位于其前面的列名
SELECT prod_name, prod_price FROM products ORDER BY prod_price DESC LIMIT 1;    # 找到最昂贵的物品；
                                                     # ORDER BY 位于 FROM 之后，LIMIT 位于 ORDER BY 之后；
```

### WHERE
```sql
SELECT prod_name, prod_price FROM products WHERE prod_price = 2.50                                                      
SELECT prod_name, prod_price FROM products WHERE prod_price >= 2.50
SELECT prod_name, prod_price FROM products WHERE prod_price BETWEEN 5 AND 10;
SELECT cust_id FROM customers WHERE cust_email IS NULL;

```

*子句操作符*

| 操作符  | 说明               |
| ------- | ------------------ |
| =       | 等于               |
| <>      | 不等于             |
| !=      | 不等于             |
| <       | 小于               |
| <=      | 小于等于           |
| >       | 大于               |
| >=      | 大于等于           |
| BETWEEN | 在指定的两个值之间 |

*`AND` & `OR`* 
```sql
SELECT prod_id, prod_price, prod_name FROM products WHERE vend_id = 1003 AND prod_price <= 10; # 逻辑与
SELECT vend_id, prod_id, prod_price, prod_name FROM products WHERE vend_id = 1003 OR vend_id = 1002; # 逻辑或
```
当`AND`和`OR`在一起时，在处理`OR`之前，优先处理`AND`操作符。解决办法是使用`()`
```sql
SELECT prod_name, prod_price FROM products WHERE vend_id = 1002 OR vend_id = 1003 AND prod_price >= 10;
SELECT prod_name, prod_price FROM products WHERE (vend_id = 1002 OR vend_id = 1003) AND prod_price >= 10;
# 使用圆括号没有什么坏处，它能消除歧义
```

*`IN`*
```sql
SELECT prod_name,prod_price FROM products WHERE vend_id IN (1002, 1003) ORDER BY prod_name;
```
`IN`的功能与`OR`相当，且有更多的优点：
    - 在使用长的合法选项清单时，`IN`操作符的语法更清楚且更直观。
    - 在使用`IN`时，计算的次序更容易管理（因为使用的操作符更少）
    - `IN`操作符一般比`OR`操作符清单执行的更快。
    - `IN`的最大优点是可以包含其他`SELECT`语句，使得能够更容易动态地建立`WHERE`子句。

`NOT`，在`WHERE`子句中用来否定后跟条件的关键字
```sql
SELECT prod_name, prod_price FROM products WHERE vend_id NOT IN (1002, 1003) ORDER BY prod_name;
```
`NOT`可以和`IN`、`BETWEEN`、`EXISTS`子句结合使用，对结果取反。


### 通配符
```sql
SELECT prod_id, prod_name FROM products WHERE prod_name LIKE 'jet%'; # 检索任意以jet起头的词
SELECT prod_id, prod_name FROM products WHERE prod_name LIKE '%anvil%'; # 检索任意位置包含文本anvil的值
SELECT prod_id, prod_name FROM products WHERE prod_name LIKE '_ ton anvil'; # 与%可以匹配任意字符不一样, 
                                                                            # _ 总是匹配一个字符，不能多也不能少 
```
`%`通配符不能匹配值为`NULL`的行。
使用通配符的技巧：
    - 不要过度使用通配符。如果其他操作符能达到相同的目的，应该使用其他操作符。
    - 在确实需要使用通配符时，除非绝对有必要，否则不要把它们用在搜索模式的开始处。把通配符置于搜索模式的开始处，搜索起来是最慢的。
    - 仔细注意通配符的位置。如果放错了地方，可能不会返回想要的数据。

### 正则表达式
```sql
SELECT prod_name FROM products WHERE prod_name REGEXP '1000' ORDER BY prod_name;
SELECT prod_name FROM products WHERE prod_name REGEXP '.000' ORDER BY prod_name; # `.`匹配任意一个字符
SELECT prod_name FROM products WHERE prod_name REGEXP BINARY 'JetPack .000' # 默认不匹配大小写, 使用 BINARY 来区分
SELECT prod_name FROM products WHERE prod_name REGEXP '1000|2000|3000'; # 进行OR匹配
SELECT prod_name FROM products WHERE prod_name REGEXP '[123] ton'; # 匹配任意几个字符, 指定一组用[和]括起来的字符
SELECT prod_name FROM products WHERE prod_name REGEXP '1|2|3 ton'; # 区别于上面的[123] ton,这里匹配的是1, 2, 3 ton 
SELECT prod_name FROM products WHERE prod_name REGEXP '[1-5] ton'; # 匹配范围  
SELECT prod_name FROM products WHERE prod_name REGEXP '\\.'; # 匹配特殊字符, 需要使用转义符
                                                             # Mysql要求两个反斜杠(Mysql自己解释一个,正则表达式库解释一个)  
SELECT prod_name FROM products WHERE prod_name REGEXP '[:alnum:]'; # 匹配字符类,更多参考p58 
SELECT prod_name FROM products WHERE prod_name REGEXP '\\([0-9] sticks?\\)'; # sticks? 匹配stick和sticks 
```
重复元字符

| 元字符 | 说明                       |
| ------ | -------------------------- |
| *      | 0个或多个匹配              |
| +      | 1个或多个匹配(等于{1,})    |
| ?      | 0个或1个匹配(等于{0,1})    |
| {n}    | 指定数目的匹配             |
| {n,}   | 不少于指定数目的匹配       |
| {n,m}  | 匹配数目的范围(m不超过255) |

定位元字符

| 元字符  | 说明       |
| ------- | ---------- |
| ^       | 文本的开始 |
| $       | 文本的结尾 |
| [[:<:]] | 词的开始   |
| [[:>:]] | 词的结尾   |

`^` 有两种用法，在集合中（用`[`和`]`定义），用它来否定该集合，否则，用来指串的开始。

简单的正则表达示测试
```sql
SELECT 'hello' REGEXP '[a-zA-Z]' # 验证字符是否符合正则
```
条件符合时结果为1，条件不符合时结果为0；

### 计算字段
```sql
SELECT Concat(vend_name, ' (', vend_country, ')') FROM vendors ORDER BY vend_name; # 拼接字段Concatenate, 将值连接到一起构成单个值
SELECT Concat(vend_name, ' (', vend_country, ')') AS vend_title FROM vendors ORDER BY vend_name; # 别名alias
SELECT Concat(RTrim(vend_name), ' (', RTrim(vend_country), ')') AS vend_title FROM vendors ORDER BY vend_name; # 去除左边LTrim(), 右边RTrim(), 两边Trim()的空格
```
MySQL 算术操作符

| 操作符 | 说明 |
| ------ | ---- |
| +      | 加   |
| -      | 减   |
| *      | 乘   |
| /      | 除   |


### 数据处理
```sql
SELECT vend_name, Upper(vend_name) AS vend_name_upcase FROM vendors ORDER BY vend_name;
SELECT cust_name, cust_contact FROM customers WHERE Soundex(cust_contact) = Soundex('Y. Lie'); # 比较发音字符
```
常用文本处理函数

| 函数        | 说明              |
| ----------- | ----------------- |
| Left()      | 返回串左边的字符  |
| Length()    | 返回串的长度      |
| Locate()    | 找出串的一个子串  |
| Lower()     | 将串转换为小写    |
| LTrim()     | 去除串左边的空格  |
| Right()     | 返回串右边的字符  |
| RTrim()     | 去除串右边的空格  |
| Soundex()   | 返回串的SOUNDEX值 |
| SubString() | 返回子串的字符    |
| Upper()     | 将串转换为大写    |

```sql
SELECT cust_id, order_num FROM orders WHERE Date(order_date) = '2005-09-01';
SELECT cust_id, order_num FROM orders WHERE Date(order_date) BETWEEN '2005-09-01' AND '2005-09-30';
SELECT cust_id, order_num FROM orders WHERE Year(order_date) = '2005' AND Month(order_date) = '09';
```
常用日期和时间处理函数

| 函数          | 说明                           |
| ------------- | ------------------------------ |
| AddDate()     | 增加一个日期（天、周等）       |
| AddTime()     | 增加一个时间                   |
| CurDate()     | 返回当前日期                   |
| CurTime()     | 返回当前日间                   |
| Date()        | 返回日期时间的日期部分         |
| DateDiff()    | 计算两个日期之差               |
| Date_Add()    | 高度灵活的日期运算函数         |
| Date_Format() | 返回一个格式化的日期或时间串   |
| Day()         | 返回一个日期的天数部分         |
| DayOfWeek()   | 对于一个日期，返回对应的星期几 |
| Hour()        | 返回一个时间的小时部分         |
| Minute()      | 返回一个时间的分钟部分         |
| Month()       | 返回一个日期的月数部分         |
| Now()         | 返回当前日期和时间             |
| Second()      | 返回一个时间的秒部分           |
| Time()        | 返回一个日期的时间部分         |
| Year()        | 返回一个日期的年份部分         |



## 何时使用单引号？
单引号用来限定字符串。如果将值与串类型的列进行比较，则需要限定引号。
用来与数值列进行比较的值不需要引号。