[TOC]

# 题目
1. 查询每门课程被选修的学生数



# 解释

```mysql
mysql> SELECT CId, COUNT(*) FROM SC  GROUP BY CId;
+------+----------+
| CId  | COUNT(*) |
+------+----------+
| 01   |        6 |
| 02   |        6 |
| 03   |        6 |
+------+----------+
3 rows in set (0.00 sec)
```


# 总结

