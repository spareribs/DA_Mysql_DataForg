[TOC]

# 题目
成绩不重复，查询选修「张三」老师所授课程的学生中，成绩最高的学生信息及其成绩





# 解释

```mysql
mysql> SELECT CId FROM Course WHERE TId IN (SELECT TId FROM Teacher WHERE Tname = "张三");
+------+
| CId  |
+------+
| 02   |
+------+
1 row in set (0.00 sec)
```

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
mysql> SELECT CId, MAX(score) FROM SC GROUP BY CId HAVING CId IN (SELECT CId FROM Course WHERE TId IN (SELECT TId FROM Teacher WHERE Tname = "张三"));
+------+------------+
| CId  | MAX(score) |
+------+------------+
| 02   |       90.0 |
+------+------------+
1 row in set (0.00 sec)
```

我去这时候我卡住了，学生信息怎么办？被我搞丢了，这时候神奇的事情来了， 排序 + MAX

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

