[TOC]

# 题目
1. 按平均成绩从高到低显示所有学生的所有课程的成绩以及平均成绩



# 解释

首先，分组统计得到平均成绩

```mysql
mysql> SELECT SId, AVG(score) AS avgscore FROM SC GROUP BY SId;
+------+----------+
| SId  | avgscore |
+------+----------+
| 01   | 89.66667 |
| 02   | 70.00000 |
| 03   | 80.00000 |
| 04   | 33.33333 |
| 05   | 81.50000 |
| 06   | 32.50000 |
| 07   | 93.50000 |
+------+----------+
7 rows in set (0.00 sec)
```

然后，将课程成绩和平均成绩结合起来进行排序

```mysql
mysql> SELECT SC.*, biao1.avgscore FROM SC LEFT JOIN (SELECT SId, AVG(score) AS avgscore FROM SC GROUP BY SId) AS biao1 ON SC.SId=biao1.SId ORDER BY biao1.avgscore DESC;
+------+------+-------+----------+
| SId  | CId  | score | avgscore |
+------+------+-------+----------+
| 07   | 03   |  98.0 | 93.50000 |
| 07   | 02   |  89.0 | 93.50000 |
| 01   | 01   |  80.0 | 89.66667 |
| 01   | 02   |  90.0 | 89.66667 |
| 01   | 03   |  99.0 | 89.66667 |
| 05   | 01   |  76.0 | 81.50000 |
| 05   | 02   |  87.0 | 81.50000 |
| 03   | 01   |  80.0 | 80.00000 |
| 03   | 02   |  80.0 | 80.00000 |
| 03   | 03   |  80.0 | 80.00000 |
| 02   | 01   |  70.0 | 70.00000 |
| 02   | 02   |  60.0 | 70.00000 |
| 02   | 03   |  80.0 | 70.00000 |
| 04   | 01   |  50.0 | 33.33333 |
| 04   | 02   |  30.0 | 33.33333 |
| 04   | 03   |  20.0 | 33.33333 |
| 06   | 01   |  31.0 | 32.50000 |
| 06   | 03   |  34.0 | 32.50000 |
+------+------+-------+----------+
18 rows in set (0.00 sec)
```

# 总结

题目不难，主要是一些过程和思路梳理清楚


# 后记

其实没有固定的答案，结构更简单，思路更清晰，查询效率更快的方法，欢迎留言，我们一起学习，一起进步~~