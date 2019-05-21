[TOC]

# 题目
21. 求每门课程的学生人数

# 解释

```mysql
mysql> SELECT CId, COUNT(CId) AS `学生人数` FROM SC GROUP BY CId;  
+------+--------------+
| CId  | 学生人数     |
+------+--------------+
| 01   |            6 |
| 02   |            6 |
| 03   |            6 |
+------+--------------+
3 rows in set (0.01 sec)
```





# 总结

