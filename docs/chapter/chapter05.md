[TOC]

# 题目
1. 查询「李」姓老师的数量 



# 解释

明确需要查询的数据表：教师表（Teacher）

这道题目简单

```mysql
mysql> SELECT COUNT(*) FROM Teacher WHERE Tname LIKE '李%';
+----------+
| COUNT(*) |
+----------+
|        1 |
+----------+
1 row in set (0.00 sec)
```



这一波题目主要考察是：

1. WHERE LIKE的使用



# 后记

其实没有固定的答案，结构更简单，思路更清晰，查询效率更快的方法，欢迎留言，我们一起学习，一起进步~~