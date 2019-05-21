[TOC]

# 题目
1. 查询选修了全部课程的学生信息



# 解释

```mysql
mysql> SELECT SId AS countcid FROM SC GROUP BY SId HAVING countcid >= 2;          
+----------+
| countcid |
+----------+
| 02       |
| 03       |
| 04       |
| 05       |
| 06       |
| 07       |
+----------+
6 rows in set (0.00 sec)
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

