## [判断记录是否存在,不存在则插入存在则更新的场景](https://my.oschina.net/iceman/blog/53735)
创建表
```sql
CREATE TABLE `clients2` (
  `client_id` int(8) NOT NULL AUTO_INCREMENT,
  `client_name` varchar(25) DEFAULT NULL,
  `client_type` int(8) DEFAULT NULL,
  PRIMARY KEY (`client_id`)
) ENGINE=InnoDB AUTO_INCREMENT=6 DEFAULT CHARSET=utf8
```

不存在则插入存在则更新的场景
```sql
# 如果表中不存在则插入指定值，如果存在则给`client_type`增加1
INSERT INTO clients (clients.`client_id`, clients.`client_name`, clients.`client_type`) VALUES (1, "Lou12", 3) ON DUPLICATE KEY UPDATE clients.`client_type`=clients.`client_type`+1;
```

https://dev.mysql.com/doc/refman/8.0/en/insert-on-duplicate.html
