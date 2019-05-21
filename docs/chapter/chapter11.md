[TOC]

# 题目
1. 查询两门及其以上不及格课程的同学的学号，姓名及其平均成绩



# 解释

首先是查询不及格的同学

```mysql
mysql> SELECT SId,score FROM SC WHERE score < 60;
+------+-------+
| SId  | score |
+------+-------+
| 04   |  50.0 |
| 04   |  30.0 |
| 04   |  20.0 |
| 06   |  31.0 |
| 06   |  34.0 |
+------+-------+
5 rows in set (0.00 sec)
```

分组统计超过2门不及格及平均成绩

```mysql
mysql> SELECT SId, COUNT(SId) AS countsid, AVG(score) AS avgscore FROM SC WHERE score < 60 GROUP BY SId HAVING countsid >= 2;
+------+----------+----------+
| SId  | countsid | avgscore |
+------+----------+----------+
| 04   |        3 | 33.33333 |
| 06   |        2 | 32.50000 |
+------+----------+----------+
2 rows in set (0.00 sec)
```

最后得到学生的信息

```
mysql> SELECT biao1.SId, Student.Sname, biao1.avgscore FROM Student, (SELECT SId, COUNT(SId) AS countsid, AVG(score) AS avgscore FROM SC WHERE score < 60 GROUP BY SId HAVING countsid >= 2) AS biao1 WHERE Student.SId = biao1.SId;
+------+--------+----------+
| SId  | Sname  | avgscore |
+------+--------+----------+
| 04   | 李云   | 33.33333 |
| 06   | 吴兰   | 32.50000 |
+------+--------+----------+
2 rows in set (0.00 sec)
```



# 总结

