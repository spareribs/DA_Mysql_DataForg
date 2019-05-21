[TOC]

# 题目
1. 查询下月过生日的学生



# 解释

先获取到下一个月

```mysql
mysql> SELECT MONTH(DATE_ADD(CURDATE(), INTERVAL 1 MONTH)); 
+----------------------------------------------+
| MONTH(DATE_ADD(CURDATE(), INTERVAL 1 MONTH)) |
+----------------------------------------------+
|                                            6 |
+----------------------------------------------+
1 row in set (0.00 sec)
```

然后通过月份过滤出下个月

```mysql
mysql> SELECT * FROM Student WHERE MONTH(Sage) = MONTH(DATE_ADD(CURDATE(), INTERVAL 1 MONTH)); 
Empty set (0.00 sec)
```

参考答案：有点没看明白

```mysql
mysql> SELECT * FROM Student WHERE EXTRACT(YEAR_MONTH FROM Student.Sage)=EXTRACT(YEAR_MONTH FROM DATE_ADD(CURDATE(),INTERVAL 1 MONTH));
Empty set (0.00 sec)
```

# 总结

