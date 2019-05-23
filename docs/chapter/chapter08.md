[TOC]

# 题目
1. 查询至少有一门课与学号为" 01 "的同学所学相同的同学的信息



# 解释

明确需要查询的数据表：学生表（`Student`）和成绩表（`SC`）

首先，搜索出01同学学习的课程

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

然后，S成绩表（`SC`）查找存在01同学课程CID的SID

```mysql
mysql> SELECT DISTINCT SId FROM SC WHERE CId IN (SELECT CId FROM SC WHERE SId = "01");
+------+
| SId  |
+------+
| 01   |
| 02   |
| 03   |
| 04   |
| 05   |
| 06   |
| 07   |
+------+
7 rows in set (0.00 sec)
```

最后，与学生表（`Student`）进行左连接，得到结果

```mysql
mysql> SELECT Student.* FROM Student INNER JOIN (SELECT DISTINCT SId FROM SC WHERE CId IN (SELECT CId FROM SC WHERE SId = "01")) AS biao1 ON Student.SId=biao1.SId;
+------+--------+---------------------+------+
| SId  | Sname  | Sage                | Ssex |
+------+--------+---------------------+------+
| 01   | 赵雷   | 1990-01-01 00:00:00 | 男   |
| 02   | 钱电   | 1990-12-21 00:00:00 | 男   |
| 03   | 孙风   | 1990-05-20 00:00:00 | 男   |
| 04   | 李云   | 1990-08-06 00:00:00 | 男   |
| 05   | 周梅   | 1991-12-01 00:00:00 | 女   |
| 06   | 吴兰   | 1992-03-01 00:00:00 | 女   |
| 07   | 郑竹   | 1989-07-01 00:00:00 | 女   |
+------+--------+---------------------+------+
7 rows in set (0.00 sec)
```



# 总结

这一波题目主要考察是：

1. DISTINCT
2. INNER JOIN

# 后记

其实没有固定的答案，结构更简单，思路更清晰，查询效率更快的方法，欢迎留言，我们一起学习，一起进步~~

