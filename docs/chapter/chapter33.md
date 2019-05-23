[TOC]

# 题目
1. 成绩不重复，查询选修「张三」老师所授课程的学生中，成绩最高的学生信息及其成绩

# 解释

首先，通过教师表和课程表查询到张三老师的课程CId

```mysql
mysql> SELECT CId FROM Course WHERE TId IN (SELECT TId FROM Teacher WHERE Tname = "张三");
+------+
| CId  |
+------+
| 02   |
+------+
1 row in set (0.00 sec)
```

然后，然后通过成绩表获取每一门课程的最高分

```mysql
mysql> SELECT CId, MAX(score) FROM SC GROUP BY CId;
+------+------------+
| CId  | MAX(score) |
+------+------------+
| 01   |       80.0 |
| 02   |       90.0 |
| 03   |       99.0 |
+------+------------+
3 rows in set (0.00 sec)
```

```mysql

mysql> SELECT CId, SId, MAX(score) FROM SC GROUP BY CId,SId HAVING CId IN (SELECT CId FROM Course WHERE TId IN (SELECT TId FROM Teacher WHERE Tname = "张三"));
+------+------+------------+
| CId  | SId  | MAX(score) |
+------+------+------------+
| 02   | 01   |       90.0 |
| 02   | 02   |       60.0 |
| 02   | 03   |       80.0 |
| 02   | 04   |       30.0 |
| 02   | 05   |       87.0 |
| 02   | 07   |       89.0 |
+------+------+------------+
6 rows in set (0.00 sec)
```

我发现我的方法已经非常非常复杂了，我停下来看了参考答案~~~

以上做了一个错误的示范，有时候思路卡住了换个方法，也是可以的~~

万能的笛卡儿积，简单省事

```mysql
mysql> SELECT  Student.*, SC.score FROM Student, Course, Teacher, SC WHERE Course.CId=SC.CId and Course.TId=Teacher.TId and Teacher.Tname='张三' AND  Student.SId =SC.SId LIMIT 1;   
+------+--------+---------------------+------+-------+
| SId  | Sname  | Sage                | Ssex | score |
+------+--------+---------------------+------+-------+
| 01   | 赵雷   | 1990-01-01 00:00:00 | 男   |  90.0 |
+------+--------+---------------------+------+-------+
1 row in set (0.00 sec)
```

# 总结

1. 新的用法 LIMIT

# 后记

其实没有固定的答案，结构更简单，思路更清晰，查询效率更快的方法，欢迎留言，我们一起学习，一起进步~~

