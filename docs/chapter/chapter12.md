[TOC]

# 题目
1. 检索" 01 "课程分数小于 60，按分数降序排列的学生信息

# 解释

这个题目相对简单，先条件过滤，然后排序即可

```mysql
mysql> SELECT * FROM SC WHERE CId = "01" AND score < 60 ORDER BY score DESC;
+------+------+-------+
| SId  | CId  | score |
+------+------+-------+
| 04   | 01   |  50.0 |
| 06   | 01   |  31.0 |
+------+------+-------+
2 rows in set (0.00 sec)
```


# 总结

# 后记

其实没有固定的答案，结构更简单，思路更清晰，查询效率更快的方法，欢迎留言，我们一起学习，一起进步~~