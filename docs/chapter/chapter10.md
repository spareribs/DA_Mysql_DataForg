[TOC]

# 题目
1. 查询没学过"张三"老师讲授的任一门课程的学生姓名



# 解释

首选，查询张三老师的课程

```mysql
mysql> SELECT CId FROM Course WHERE TId IN (SELECT TId FROM Teacher WHERE Teacher.Tname = "张三");
+------+
| CId  |
+------+
| 02   |
+------+
1 row in set (0.00 sec)
```

然后，使用学生和课程做左连接，得到了所有的可能性

```mysql
mysql> SELECT Student.SId, biao1.CId FROM Student, (SELECT CId FROM Course WHERE TId IN (SELECT TId FROM Teacher WHERE Teacher.Tname = "张三")) AS biao1;
+------+------+
| SId  | CId  |
+------+------+
| 01   | 02   |
| 02   | 02   |
| 03   | 02   |
| 04   | 02   |
| 05   | 02   |
| 06   | 02   |
| 07   | 02   |
| 09   | 02   |
| 10   | 02   |
| 11   | 02   |
| 12   | 02   |
| 13   | 02   |
+------+------+
12 rows in set (0.01 sec)
```

通过左连接成绩表得到所有参与过的同学的信息

```mysql
mysql> SELECT biao2.SId FROM (SELECT Student.SId, biao1.CId FROM Student, (SELECT CId FROM Course WHERE TId IN (SELECT TId FROM Teacher WHERE Teacher.Tname = "张三")) AS biao1) AS biao2 INNER JOIN SC ON biao2.SId=SC.SId AND biao2.CId=SC.CId;
+------+
| SId  |
+------+
| 01   |
| 02   |
| 03   |
| 04   |
| 05   |
| 07   |
+------+
6 rows in set (0.00 sec)
```

最后，查询表格，不在这个范围内的

```mysql

mysql> SELECT * FROM Student WHERE SId NOT IN (SELECT biao2.SId FROM (SELECT Student.SId, biao1.CId FROM Student, (SELECT CId FROM Course WHERE TId IN (SELECT TId FROM Teacher WHERE Teacher.Tname = "张三")) AS biao1) AS biao2 INNER JOIN SC ON biao2.SId=SC.SId AND biao2.CId=SC.CId);
+------+--------+---------------------+------+
| SId  | Sname  | Sage                | Ssex |
+------+--------+---------------------+------+
| 06   | 吴兰   | 1992-03-01 00:00:00 | 女   |
| 09   | 张三   | 2017-12-20 00:00:00 | 女   |
| 10   | 李四   | 2017-12-25 00:00:00 | 女   |
| 11   | 李四   | 2017-12-30 00:00:00 | 女   |
| 12   | 赵六   | 2017-01-01 00:00:00 | 女   |
| 13   | 孙七   | 2018-01-01 00:00:00 | 女   |
+------+--------+---------------------+------+
6 rows in set (0.00 sec)
```



# 后记

其实没有固定的答案，结构更简单，思路更清晰，查询效率更快的方法，欢迎留言，我们一起学习，一起进步~~

