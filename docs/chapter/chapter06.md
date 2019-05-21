[TOC]

# 题目
1. 查询学过「张三」老师授课的同学的信息 



# 解释

```mysql
mysql> SELECT TId FROM Teacher WHERE Tname="张三";     
+------+
| TId  |
+------+
| 01   |
+------+
1 row in set (0.00 sec)
```

个人实现的方法：

```mysql
mysql> SELECT * FROM Student WHERE Student.SId IN (SELECT SId FROM SC WHERE SC.CId IN (SELECT CId FROM Course WHERE TId IN (SELECT TId FROM Teacher WHERE Tname="张三")));
+------+--------+---------------------+------+
| SId  | Sname  | Sage                | Ssex |
+------+--------+---------------------+------+
| 01   | 赵雷   | 1990-01-01 00:00:00 | 男   |
| 02   | 钱电   | 1990-12-21 00:00:00 | 男   |
| 03   | 孙风   | 1990-05-20 00:00:00 | 男   |
| 04   | 李云   | 1990-08-06 00:00:00 | 男   |
| 05   | 周梅   | 1991-12-01 00:00:00 | 女   |
| 07   | 郑竹   | 1989-07-01 00:00:00 | 女   |
+------+--------+---------------------+------+
6 rows in set (0.00 sec)
```

答案中的方法：

```mysql
mysql> SELECT Student.* FROM Teacher, Course, Student, SC WHERE Teacher.Tname='张三'  AND Teacher.TId=Course.TId AND Course.CId=SC.CId AND SC.SId=Student.SId;
+------+--------+---------------------+------+
| SId  | Sname  | Sage                | Ssex |
+------+--------+---------------------+------+
| 01   | 赵雷   | 1990-01-01 00:00:00 | 男   |
| 02   | 钱电   | 1990-12-21 00:00:00 | 男   |
| 03   | 孙风   | 1990-05-20 00:00:00 | 男   |
| 04   | 李云   | 1990-08-06 00:00:00 | 男   |
| 05   | 周梅   | 1991-12-01 00:00:00 | 女   |
| 07   | 郑竹   | 1989-07-01 00:00:00 | 女   |
+------+--------+---------------------+------+
6 rows in set (0.00 sec)
```



# 总结

