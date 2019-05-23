[TOC]

# 题目
1. 查询每门课程的平均成绩，结果按平均成绩降序排列，平均成绩相同时，按课程编号升序排列

# 解释

题目不难，先分组后排序

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

# 后记

其实没有固定的答案，结构更简单，思路更清晰，查询效率更快的方法，欢迎留言，我们一起学习，一起进步~~