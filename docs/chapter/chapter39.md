[TOC]

# 题目
1. 查询选修了全部课程的学生信息



# 解释

与题38类似

```mysql
mysql> SELECT SId, COUNT(SId) AS countcid FROM SC GROUP BY SId HAVING countcid = (SELECT COUNT(*) FROM Course);
+------+----------+
| SId  | countcid |
+------+----------+
| 01   |        3 |
| 02   |        3 |
| 03   |        3 |
| 04   |        3 |
+------+----------+
4 rows in set (0.00 sec)
```

# 总结

# 后记

其实没有固定的答案，结构更简单，思路更清晰，查询效率更快的方法，欢迎留言，我们一起学习，一起进步~

