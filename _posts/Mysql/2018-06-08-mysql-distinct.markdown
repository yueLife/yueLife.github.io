---
layout: post
title: Mysql 的 DISTINCT 关键字
date: 2018-06-08
tag: Mysql
---

关键词 ```DISTINCT``` 用于返回唯一不同的值。一般只用它来返回不重复记录的条数，而不是用它来返回不重记录的所有值。

首先，新建一张users表，并插入几条记录。
```bash
CREATE TABLE `users` (
  `id` int(10) NOT NULL AUTO_INCREMENT comment '主键ID',
  `user_name` varchar(100) DEFAULT NULL COMMENT '用户名',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=1 DEFAULT CHARSET=utf8;
```

查询users 表中所有记录：
```bash
mysql> SELECT user_name FROM users;
+-----------+
| user_name |
+-----------+
| 张三      |
| 李四      |
| 王五      |
| 赵六      |
| 张三      |
+-----------+
5 rows in set
```

1.查询users 表中user_name 不重复的记录：
```bash
mysql> SELECT DISTINCT user_name FROM users;
+-----------+
| user_name |
+-----------+
| 张三      |
| 李四      |
| 王五      |
| 赵六      |
+-----------+
4 rows in set
```

查询多个字段时（会提示错误，因为```DISTINCT```必须放在开头）：
```bash
mysql> SELECT id,DISTINCT user_name FROM users;
1064 - You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use near 'DISTINCT user_name FROM users' at line 1

mysql> SELECT DISTINCT user_name,id FROM users;
+-----------+----+
| user_name | id |
+-----------+----+
| 张三      |  1 |
| 李四      |  2 |
| 王五      |  3 |
| 赵六      |  4 |
| 张三      |  5 |
+-----------+----+
5 rows in set
```
实际上返回的是 id与user_name 同时不相同的结果，也就是```DISTINCT```同时作用了两个字段，必须得id 与user_name 都相同的才被排除了。

2.使用```COUNT()```统计不重复的记录：
```bash
mysql> SELECT COUNT(DISTINCT user_name) FROM users;
+---------------------------+
| COUNT(DISTINCT user_name) |
+---------------------------+
|                         4 |
+---------------------------+
1 row in set
```
