[TOC]

# 题目
1. 成绩有重复的情况下，查询选修「张三」老师所授课程的学生中，成绩最高的学生信息及其成绩



# 解释

```mysql
mysql> SELECT CId FROM Course WHERE TId IN (SELECT TId FROM Teacher WHERE Tname = "张三");
+------+
| CId  |
+------+
| 02   |
+------+
1 row in set (0.00 sec)
```

```mysql
mysql> SELECT CId, MAX(score) FROM SC GROUP BY CId;
+------+------------+
| CId  | MAX(score) |
+------+------------+
| 01   |       80.0 |
| 02   |       90.0 |
| 03   |       99.0 |
+------+------------+
3 rows in set (0.00 sec)
```


# 总结

# 后记

其实没有固定的答案，结构更简单，思路更清晰，查询效率更快的方法，欢迎留言，我们一起学习，一起进步~~