[TOC]

# 题目
1. 查询「李」姓老师的数量 



# 解释

```mysql
mysql> SELECT * FROM Teacher WHERE Tname LIKE '李%';
+------+--------+
| TId  | Tname  |
+------+--------+
| 02   | 李四   |
+------+--------+
1 row in set (0.00 sec)
```



# 总结