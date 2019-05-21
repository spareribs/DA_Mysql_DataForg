[TOC]

# 题目
1. 查询男生、女生人数



# 解释

```mysql
mysql> SELECT Ssex,Count(*) FROM Student GROUP BY Ssex;  
+------+----------+
| Ssex | Count(*) |
+------+----------+
| 女   |        8 |
| 男   |        4 |
+------+----------+
2 rows in set (0.00 sec)
```

# 总结

