[TOC]

# 题目
1. 查询出只选修两门课程的学生学号和姓名



# 解释

首先，通过分组计算出每个学生选修的课程数

```mysql
mysql> SELECT SId, COUNT(*) AS  countsid FROM SC  GROUP BY SId HAVING countsid = 2;
+------+----------+
| SId  | countsid |
+------+----------+
| 05   |        2 |
| 06   |        2 |
| 07   |        2 |
+------+----------+
3 rows in set (0.00 sec)
```

然后，左连接到学生表得到结果

```mysql
mysql> SELECT Student.SId, Student.Sname FROM (SELECT SId, COUNT(*) AS countsid FROM SC GROUP BY SId HAVING countsid = 2) AS biao1 INNER JOIN Student ON Student.SId = biao1.SId;  
+------+--------+
| SId  | Sname  |
+------+--------+
| 05   | 周梅   |
| 06   | 吴兰   |
| 07   | 郑竹   |
+------+--------+
3 rows in set (0.00 sec)
```



# 总结

# 后记

其实没有固定的答案，结构更简单，思路更清晰，查询效率更快的方法，欢迎留言，我们一起学习，一起进步~~