---
layout: post
title: Mysql 的 count 函数
date: 2018-06-08
tag: Mysql
---

`count()`函数是用来统计表中记录的一个函数，返回匹配条件的行数。

`count()`语法：
>1、`count(*)`：统计表中所有列，返回记录数，在统计结果的时候，不会忽略列值为NULL的记录。  
>2、`count(1)`：忽略所有列，1表示一个固定值，也可以用`count(2)`、`count(3)`代替，在统计结果的时候，不会忽略列值为NULL的记录。  
>3、`count(列名)`：只包括列名指定列，返回指定列的记录数，在统计结果的时候，会忽略列值为NULL的记录（不包括空字符串和0），即列值为NULL的记录不统计在内。  
>4、`count(distinct 列名)`：只包括列名指定列，返回指定列的不同值的记录数，在统计结果的时候，在统计结果的时候，会忽略列值为NULL的记录（不包括空字符串和0），即列值为NULL的记录不统计在内。

1.在count 不重复的记录的时候能用到，比如`SELECT COUNT( DISTINCT id ) FROM tablename;` 就是计算talbebname表中id不同的记录有多少条。

2,在需要返回记录不同的id的具体值的时候可以用，比如 `SELECT DISTINCT id FROM tablename;` ，返回talbebname表中不同的id的具体的值。

3.上面的情况2对于需要返回mysql表中2列以上的结果时会有歧义，比如 `SELECT DISTINCT id, type FROM tablename;`，实际上返回的是 id与type同时不相同的结果,也就是 `DISTINCT` 同时作用了两个字段，必须得id与type都相同的才被排除了,与我们期望的结果不一样。  

4.这时候可以考虑使用group_concat函数来进行排除,不过这个mysql函数是在mysql4.1以上才支持的。

5.其实还有另外一种解决方式,就是使用 `SELECT id, type, count(DISTINCT id) FROM tablename;` ，虽然这样的返回结果多了一列无用的count数据（或许你就需要这个我说的无用数据）。返回的结果是，只有id不同的所有结果和上面的4类型可以互补使用,就是看你需要什么样的数据了。