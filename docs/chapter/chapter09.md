[TOC]

# 题目
1. 查询和" 01 "号的同学学习的课程完全相同的其他同学的信息



# 解释

明确需要查询的数据表：成绩表（`SC`）和学生表（`Student`）

首先，查询01同学所有的课程

```mysql
mysql> SELECT CId FROM SC WHERE SId = "01";
+------+
| CId  |
+------+
| 01   |
| 02   |
| 03   |
+------+
3 rows in set (0.00 sec)
```

然后，得到所有学生和所有课程的组合：

```mysql
mysql> SELECT Student.SId, biao1.CId FROM Student, (SELECT CId FROM SC WHERE SId = "01") AS biao1;
+------+------+
| SId  | CId  |
+------+------+
| 01   | 01   |
| 01   | 02   |
| 01   | 03   |
| 02   | 01   |
| 02   | 02   |
| 02   | 03   |
| 03   | 01   |
| 03   | 02   |
| 03   | 03   |
| 04   | 01   |
| 04   | 02   |
| 04   | 03   |
| 05   | 01   |
| 05   | 02   |
| 05   | 03   |
| 06   | 01   |
| 06   | 02   |
| 06   | 03   |
| 07   | 01   |
| 07   | 02   |
| 07   | 03   |
| 09   | 01   |
| 09   | 02   |
| 09   | 03   |
| 10   | 01   |
| 10   | 02   |
| 10   | 03   |
| 11   | 01   |
| 11   | 02   |
| 11   | 03   |
| 12   | 01   |
| 12   | 02   |
| 12   | 03   |
| 13   | 01   |
| 13   | 02   |
| 13   | 03   |
+------+------+
36 rows in set (0.00 sec)
```

接着，与课程表左连接

```mysql
mysql> SELECT * FROM (SELECT Student.SId, biao1.Cid FROM Student, (SELECT CId FROM SC WHERE SId = "01") AS biao1) AS biao2 LEFT JOIN SC ON SC.SId=biao2.SId;
+------+------+------+------+-------+
| SId  | CId  | SId  | CId  | score |
+------+------+------+------+-------+
| 01   | 01   | 01   | 01   |  80.0 |
| 01   | 01   | 01   | 02   |  90.0 |
| 01   | 01   | 01   | 03   |  99.0 |
| 01   | 02   | 01   | 01   |  80.0 |
| 01   | 02   | 01   | 02   |  90.0 |
| 01   | 02   | 01   | 03   |  99.0 |
| 01   | 03   | 01   | 01   |  80.0 |
| 01   | 03   | 01   | 02   |  90.0 |
| 01   | 03   | 01   | 03   |  99.0 |
| 02   | 01   | 02   | 01   |  70.0 |
| 02   | 01   | 02   | 02   |  60.0 |
| 02   | 01   | 02   | 03   |  80.0 |
| 02   | 02   | 02   | 01   |  70.0 |
| 02   | 02   | 02   | 02   |  60.0 |
| 02   | 02   | 02   | 03   |  80.0 |
| 02   | 03   | 02   | 01   |  70.0 |
| 02   | 03   | 02   | 02   |  60.0 |
| 02   | 03   | 02   | 03   |  80.0 |
| 03   | 01   | 03   | 01   |  80.0 |
| 03   | 01   | 03   | 02   |  80.0 |
| 03   | 01   | 03   | 03   |  80.0 |
| 03   | 02   | 03   | 01   |  80.0 |
| 03   | 02   | 03   | 02   |  80.0 |
| 03   | 02   | 03   | 03   |  80.0 |
| 03   | 03   | 03   | 01   |  80.0 |
| 03   | 03   | 03   | 02   |  80.0 |
| 03   | 03   | 03   | 03   |  80.0 |
| 04   | 01   | 04   | 01   |  50.0 |
| 04   | 01   | 04   | 02   |  30.0 |
| 04   | 01   | 04   | 03   |  20.0 |
| 04   | 02   | 04   | 01   |  50.0 |
| 04   | 02   | 04   | 02   |  30.0 |
| 04   | 02   | 04   | 03   |  20.0 |
| 04   | 03   | 04   | 01   |  50.0 |
| 04   | 03   | 04   | 02   |  30.0 |
| 04   | 03   | 04   | 03   |  20.0 |
| 05   | 01   | 05   | 01   |  76.0 |
| 05   | 01   | 05   | 02   |  87.0 |
| 05   | 02   | 05   | 01   |  76.0 |
| 05   | 02   | 05   | 02   |  87.0 |
| 05   | 03   | 05   | 01   |  76.0 |
| 05   | 03   | 05   | 02   |  87.0 |
| 06   | 01   | 06   | 01   |  31.0 |
| 06   | 01   | 06   | 03   |  34.0 |
| 06   | 02   | 06   | 01   |  31.0 |
| 06   | 02   | 06   | 03   |  34.0 |
| 06   | 03   | 06   | 01   |  31.0 |
| 06   | 03   | 06   | 03   |  34.0 |
| 07   | 01   | 07   | 02   |  89.0 |
| 07   | 01   | 07   | 03   |  98.0 |
| 07   | 02   | 07   | 02   |  89.0 |
| 07   | 02   | 07   | 03   |  98.0 |
| 07   | 03   | 07   | 02   |  89.0 |
| 07   | 03   | 07   | 03   |  98.0 |
| 09   | 01   | NULL | NULL |  NULL |
| 09   | 02   | NULL | NULL |  NULL |
| 09   | 03   | NULL | NULL |  NULL |
| 10   | 01   | NULL | NULL |  NULL |
| 10   | 02   | NULL | NULL |  NULL |
| 10   | 03   | NULL | NULL |  NULL |
| 11   | 01   | NULL | NULL |  NULL |
| 11   | 02   | NULL | NULL |  NULL |
| 11   | 03   | NULL | NULL |  NULL |
| 12   | 01   | NULL | NULL |  NULL |
| 12   | 02   | NULL | NULL |  NULL |
| 12   | 03   | NULL | NULL |  NULL |
| 13   | 01   | NULL | NULL |  NULL |
| 13   | 02   | NULL | NULL |  NULL |
| 13   | 03   | NULL | NULL |  NULL |
+------+------+------+------+-------+
69 rows in set (0.00 sec)
```

将为NULL的同学的信息过滤出来

```mysql
mysql> SELECT DISTINCT biao2.SId FROM (SELECT Student.SId, biao1.Cid FROM Student, (SELECT CId FROM SC WHERE SId = "01") AS biao1) AS biao2 LEFT JOIN SC ON SC.SId=biao2.SId WHERE SC.SId IS NULL;
+------+
| SId  |
+------+
| 09   |
| 10   |
| 11   |
| 12   |
| 13   |
+------+
5 rows in set (0.00 sec)
```

最后，与01同学学习相同课程的小伙伴的信息就有

```mysql
mysql> SELECT * FROM Student WHERE SId NOT IN (SELECT DISTINCT biao2.SId FROM (SELECT Student.SId, biao1.Cid FROM Student, (SELECT CId FROM SC WHERE SId = "01") AS biao1) AS biao2 LEFT JOIN SC ON SC.SId=biao2.SId WHERE SC.SId IS NULL) AND SId != "01";  
+------+--------+---------------------+------+
| SId  | Sname  | Sage                | Ssex |
+------+--------+---------------------+------+
| 02   | 钱电   | 1990-12-21 00:00:00 | 男   |
| 03   | 孙风   | 1990-05-20 00:00:00 | 男   |
| 04   | 李云   | 1990-08-06 00:00:00 | 男   |
| 05   | 周梅   | 1991-12-01 00:00:00 | 女   |
| 06   | 吴兰   | 1992-03-01 00:00:00 | 女   |
| 07   | 郑竹   | 1989-07-01 00:00:00 | 女   |
+------+--------+---------------------+------+
6 rows in set (0.00 sec)
```



# 总结

这一波题目主要考察是：

1. LEFT JOIN
2. DISTINCT
3. WHERE



# 后记

其实没有固定的答案，结构更简单，思路更清晰，查询效率更快的方法，欢迎留言，我们一起学习，一起进步~~

