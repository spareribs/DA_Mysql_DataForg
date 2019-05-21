[TOC]

# 题目
1. 查询不及格的课程

# 解释

```mysql
mysql> SELECT DISTINCT SC.CId from SC where SC.score <60;           
+------+
| CId  |
+------+
| 01   |
| 02   |
| 03   |
+------+
3 rows in set (0.01 sec)
```



# 总结

