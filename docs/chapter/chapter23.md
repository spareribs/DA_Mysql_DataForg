[TOC]

# 题目
1. 查询同名同性学生名单，并统计同名人数

# 解释

首先，学生表自己做笛卡儿积，做条件判断即可得到同名同性，但是不同SId的表

```mysql
mysql> SELECT biao1.*,biao2.* FROM Student AS biao1,Student AS biao2 WHERE biao1.Sname=biao2.Sname AND biao1.Ssex=biao2.Ssex AND biao1.SId != biao2.SId; 
+------+--------+---------------------+------+------+--------+---------------------+------+
| SId  | Sname  | Sage                | Ssex | SId  | Sname  | Sage                | Ssex |
+------+--------+---------------------+------+------+--------+---------------------+------+
| 11   | 李四   | 2017-12-30 00:00:00 | 女   | 10   | 李四   | 2017-12-25 00:00:00 | 女   |
| 10   | 李四   | 2017-12-25 00:00:00 | 女   | 11   | 李四   | 2017-12-30 00:00:00 | 女   |
+------+--------+---------------------+------+------+--------+---------------------+------+
2 rows in set (0.00 sec)
```

然后，通过分组即可得到结果

```mysql
mysql> SELECT Sname,Ssex,COUNT(*) FROM (SELECT biao1.* FROM Student AS biao1,Student AS biao2 WHERE biao1.Sname=biao2.Sname AND biao1.Ssex=biao2.Ssex AND biao1.SId != biao2.SId) AS biao3 GROUP BY Sname,Ssex;
+--------+------+----------+
| Sname  | Ssex | COUNT(*) |
+--------+------+----------+
| 李四   | 女   |        2 |
+--------+------+----------+
1 row in set (0.00 sec)

```

# 总结

这里是多个分组条件，也是一样的操作

# 后记

其实没有固定的答案，结构更简单，思路更清晰，查询效率更快的方法，欢迎留言，我们一起学习，一起进步~~