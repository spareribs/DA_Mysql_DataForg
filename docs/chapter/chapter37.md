[TOC]

# 题目
1. 统计每门课程的学生选修人数（超过 5 人的课程才统计）。



# 解释

分组统计结果

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


# 总结

# 后记

其实没有固定的答案，结构更简单，思路更清晰，查询效率更快的方法，欢迎留言，我们一起学习，一起进步~~