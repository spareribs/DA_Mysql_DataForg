[TOC]

# 题目
1. 检索" 01 "课程分数小于 60，按分数降序排列的学生信息



# 解释

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

