[TOC]

# 题目
1. 查询每门功成绩最好的前两名

# 解释

题目中没有说明前2名的什么信息，直接查询成绩表得到前2名

核心思想是：我们要查询的这个人，在这一门中分数比他高的少于2个人。
括号里面是查询在这一门中分数比他高的人的数量。

```mysql
mysql> SELECT biao1.*  FROM SC AS biao1  WHERE ( SELECT COUNT( CId ) FROM SC WHERE CId = biao1.CId AND biao1.score < score ) < 2  ORDER BY CId ASC, score DESC;
+------+------+-------+
| SId  | CId  | score |
+------+------+-------+
| 01   | 01   |  80.0 |
| 03   | 01   |  80.0 |
| 01   | 02   |  90.0 |
| 07   | 02   |  89.0 |
| 01   | 03   |  99.0 |
| 07   | 03   |  98.0 |
+------+------+-------+
6 rows in set (0.00 sec)
```



# 总结

参考文章：

- <https://blog.csdn.net/acmain_chm/article/details/4126306>
- <https://bbs.csdn.net/topics/390319304>

# 后记

其实没有固定的答案，结构更简单，思路更清晰，查询效率更快的方法，欢迎留言，我们一起学习，一起进步~~



