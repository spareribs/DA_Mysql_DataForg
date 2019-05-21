[TOC]

# 题目2
1. 查询平均成绩大于等于 60 分的同学的学生编号和学生姓名和平均成绩

# 解释



```mysql
mysql> SELECT SC.SId ,AVG(SC.score) AS avgscore FROM SC GROUP BY SC.SId HAVING avgscore>=60;           
+------+----------+
| SId  | avgscore |
+------+----------+
| 01   | 89.66667 |
| 02   | 70.00000 |
| 03   | 80.00000 |
| 05   | 81.50000 |
| 07   | 93.50000 |
+------+----------+
5 rows in set (0.00 sec)
```



```mysql
mysql> SELECT biao1.*, biao2.avgscore FROM Student AS biao1 INNER JOIN (SELECT SC.SId ,AVG(SC.score) AS avgscore FROM SC GROUP BY SC.SId HAVING avgscore>=60) AS biao2 WHERE biao1.SId = biao2.SId;
+------+--------+---------------------+------+----------+
| SId  | Sname  | Sage                | Ssex | avgscore |
+------+--------+---------------------+------+----------+
| 01   | 赵雷   | 1990-01-01 00:00:00 | 男   | 89.66667 |
| 02   | 钱电   | 1990-12-21 00:00:00 | 男   | 70.00000 |
| 03   | 孙风   | 1990-05-20 00:00:00 | 男   | 80.00000 |
| 05   | 周梅   | 1991-12-01 00:00:00 | 女   | 81.50000 |
| 07   | 郑竹   | 1989-07-01 00:00:00 | 女   | 93.50000 |
+------+--------+---------------------+------+----------+
5 rows in set (0.00 sec)
```



# 总结

这一波题目主要考察是：

1. SELECT的使用，使用AS来重命名表
2. WHERE的使用，AND多重条件
3. LEFT JOIN ... ON 的使用
4. WHERE的使用，NOT IN条件

看到一个关于链接比较好的文章，推荐 <https://segmentfault.com/a/1190000017369618>



# 后记

其实没有固定的答案，结构更简单，思路更清晰，查询效率更快的方法，欢迎留言，我们一起学习，一起进步~~