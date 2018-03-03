---
title: sql常见操作
date: 2016/10/11 20:29
toc: true
comments: true
tags:
- sql
---


## 删除字符串空格
- RTrim() 删除右边的空格
- LTrim() 删除左边的空格
- Trim() 删除左右两边的空格
```bash
SELECT Concat(RTrim(vend_name),' (', RTrim(vend_country), ')') FROM vendors ORDER BY vend_name;
```
p83


## 验证字符是否符合正则
```bash
SELECT 'hello' REGEXP '[0-9]'
```
条件符合时结果为1，条件不符合时结果为0；

## LIKE 操作符
LIKE
指示MYSQL，后跟的搜索模式利用通配符匹配而不是直接相等匹配进行比较。

## IN 操作符
（当涉及删除多条语句的时候，比起单独一条一条地删除，通过 IN 操作符来删除效率更高，亲测）
```sh
SELECT prod_name, prod_price FROM products WHERE vend_id IN (1002, 1003) ORDER BY prod_name;
```
优点：p58
- 在使用长的合法选项清单时，IN 操作符的语法更清楚且更直观。
- 在使用IN时，计算的次序更容易管理（因为使用的操作符更少）
- IN操作符一般比OR操作符清单执行更快
- IN的最大优点是包含其他SELECT语句，使得能够更动态地建立WHERE子句。


## AND 和 OR 的计算次序
SQL（像多数语言一样）在处理 OR 操作符前，优先处理 AND 操作符。
解决办法是通过使用圆括号来明确分组；p55
```sh
SLECT prod_name, prod_price FROM products WHERE (vend_id = 1002 OR vend_id = 1003) AND prod_price >= 10;
```

## 获取匹配范围的所有行
```sh
SELECT prod_name,prod_price FROM products WHERE prod_price BETWEEN 5 AND 10
```
包括了指定的开始值和结束值。（即包含5和10）；p49

## 何时使用单引号？
单引号用来限定字符串。如果将值与串类型的列进行比较，则需要限定引号。
用来与数值列进行比较的值不需要引号。

## 字句顺序
在同时使用ORDER BY 和 WHERE 字句时，应该让 ORDER BY 位于 WHERE 之后，否则会产生错误。p46

## 字句顺序
在给出 ORDER BY 字句时，应该保证它位于 FROM 字句之后。
如果使用 LIMIT ，它必须位于 ORDER BY 之后。
使用子句的次序不对将产生错误。p43

## note
页数, 以小标为准
