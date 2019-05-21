[TOC]

# 题目
1. 统计每门课程的学生选修人数（超过 5 人的课程才统计）。



# 解释

```mysql
mysql> SELECT CId, COUNT(*) AS countsid FROM SC GROUP BY CId HAVING countsid >= 5;        
+------+----------+
| CId  | countsid |
+------+----------+
| 01   |        6 |
| 02   |        6 |
| 03   |        6 |
+------+----------+
3 rows in set (0.00 sec)
```

```mysql

```

```mysql

```

```mysql

```

```mysql

```

```mysql

```



# 总结

