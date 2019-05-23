[TOC]

# 题目
21. 查询平均成绩大于等于 85 的所有学生的学号、姓名和平均成绩

# 解释

首先，查询平均成绩大于等于 85 的所有学生的编号

```mysql
mysql> SELECT SId, AVG(score) AS avgscore FROM SC GROUP BY SId HAVING avgscore > 85;  
+------+----------+
| SId  | avgscore |
+------+----------+
| 01   | 89.66667 |
| 07   | 93.50000 |
+------+----------+
2 rows in set (0.00 sec)
```

然后，与学生表做连接

```mysql
mysql> SELECT Student.SId,Student.Sname, biao1.avgscore FROM Student INNER JOiN (SELECT SId, AVG(score) AS avgscore FROM SC GROUP BY SId HAVING avgscore > 85) AS biao1 ON Student.SId=biao1.SId;
+------+--------+----------+
| SId  | Sname  | avgscore |
+------+--------+----------+
| 01   | 赵雷   | 89.66667 |
| 07   | 郑竹   | 93.50000 |
+------+--------+----------+
2 rows in set (0.00 sec)
```

# 总结

# 后记

其实没有固定的答案，结构更简单，思路更清晰，查询效率更快的方法，欢迎留言，我们一起学习，一起进步~~