[TOC]

# 题目
21. 查询课程名称为「数学」，且分数低于 60 的学生姓名和分数

# 解释

首先，查询数学课程

```mysql
mysql> SELECT * FROM Course WHERE Cname = "数学";
+------+--------+------+
| CId  | Cname  | TId  |
+------+--------+------+
| 02   | 数学   | 01   |
+------+--------+------+
1 row in set (0.00 sec)
```

然后，通过成绩表，查询成绩低于60的学生SId信息

```mysql
mysql> SELECT * FROM SC WHERE CId IN (SELECT CId FROM Course WHERE Cname = "数学") AND score <60;
+------+------+-------+
| SId  | CId  | score |
+------+------+-------+
| 04   | 02   |  30.0 |
+------+------+-------+
1 row in set (0.00 sec)
```

最后，通过学生表，得到学生的姓名

```mysql
mysql> SELECT Student.Sname, biao1.score FROM Student,(SELECT * FROM SC WHERE CId IN (SELECT CId FROM Course WHERE Cname = "数学") AND score <60) AS biao1 WHERE Student.SId = biao1.SId;
+--------+-------+
| Sname  | score |
+--------+-------+
| 李云   |  30.0 |
+--------+-------+
1 row in set (0.00 sec)
```

# 总结

# 后记

其实没有固定的答案，结构更简单，思路更清晰，查询效率更快的方法，欢迎留言，我们一起学习，一起进步~~