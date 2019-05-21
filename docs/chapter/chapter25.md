[TOC]

# 题目
1. 查询每门课程的平均成绩，结果按平均成绩降序排列，平均成绩相同时，按课程编号升序排列

# 解释

首选查询平均成绩

```mysql
mysql> SELECT CId, AVG(score) AS avgscore FROM SC GROUP BY CId ORDER BY avgscore DESC, CId ASC;  
+------+----------+
| CId  | avgscore |
+------+----------+
| 02   | 72.66667 |
| 03   | 68.50000 |
| 01   | 64.50000 |
+------+----------+
3 rows in set (0.01 sec)
```

# 总结

