[TOC]

# 题目
1. 查询不及格的课程

# 解释

题目相对简单

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

# 后记

其实没有固定的答案，结构更简单，思路更清晰，查询效率更快的方法，欢迎留言，我们一起学习，一起进步~~