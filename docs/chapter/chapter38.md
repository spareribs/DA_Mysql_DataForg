[TOC]

# 题目
1. 检索至少选修两门课程的学生学号



# 解释

分组统计结果

```mysql
mysql> SELECT SId, COUNT(SId) AS countcid FROM SC GROUP BY SId HAVING countcid >= 2;  
+------+----------+
| SId  | countcid |
+------+----------+
| 01   |        3 |
| 02   |        3 |
| 03   |        3 |
| 04   |        3 |
| 05   |        2 |
| 06   |        2 |
| 07   |        2 |
+------+----------+
7 rows in set (0.00 sec)
```

# 总结

# 后记

其实没有固定的答案，结构更简单，思路更清晰，查询效率更快的方法，欢迎留言，我们一起学习，一起进步~~

