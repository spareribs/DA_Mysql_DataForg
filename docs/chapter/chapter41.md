[TOC]

# 题目
1. 按照出生日期来算，当前月日 < 出生年月的月日则，年龄减一

# 解释

获取当前月份和日期

```mysql
mysql> SELECT DATE_FORMAT(CURRENT_DATE(), "%m%d");
+-------------------------------------+
| DATE_FORMAT(CURRENT_DATE(), "%m%d") |
+-------------------------------------+
| 0523                                |
+-------------------------------------+
1 row in set (0.00 sec)
```

通过 CASE WHEN 确认是否需要减1

```mysql
mysql> SELECT Sname,Ssex,(TIMESTAMPDIFF(YEAR, Student.Sage, CURDATE()) - (CASE WHEN DATE_FORMAT(CURRENT_DATE(), "%m%d") > DATE_FORMAT(Ssex,"%m%d") THEN 0 ELSE 1 END)) AS old FROM Student;
+--------+------+------+
| Sname  | Ssex | old  |
+--------+------+------+
| 赵雷   | 男   |   28 |
| 钱电   | 男   |   27 |
| 孙风   | 男   |   28 |
| 李云   | 男   |   27 |
| 周梅   | 女   |   26 |
| 吴兰   | 女   |   26 |
| 郑竹   | 女   |   28 |
| 张三   | 女   |    0 |
| 李四   | 女   |    0 |
| 李四   | 女   |    0 |
| 赵六   | 女   |    1 |
| 孙七   | 女   |    0 |
+--------+------+------+
12 rows in set, 12 warnings (0.00 sec)
```



# 总结

# 后记

其实没有固定的答案，结构更简单，思路更清晰，查询效率更快的方法，欢迎留言，我们一起学习，一起进步~~