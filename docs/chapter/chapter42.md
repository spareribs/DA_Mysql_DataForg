[TOC]

# 题目
1. 查询本周过生日的学生
2. 查询下周过生日的学生
3. 查询本月过生日的学生
4. 查询下月过生日的学生

# 解释

## 题目1：查询本周过生日的学生

当前时间

```mysql
mysql> SELECT NOW();
+---------------------+
| NOW()               |
+---------------------+
| 2019-05-16 13:14:18 |
+---------------------+
1 row in set (0.00 sec)
```

我特意去改了一个本周生日的数据

```mysql
mysql> SELECT * FROM Student WHERE WEEK(Sage) = WEEK(CURDATE());
+------+--------+---------------------+------+
| SId  | Sname  | Sage                | Ssex |
+------+--------+---------------------+------+
| 13   | 孙七   | 2018-05-18 00:00:00 | 女   |
+------+--------+---------------------+------+
1 row in set (0.00 sec)
```



## 题目2：查询下周过生日的学生

CURDATE()： 获取当前时间

DATE_ADD(CURDATE(), INTERVAL 1 WEEK)：当前时间基础上增加一周

WEEK(DATE_ADD(CURDATE(), INTERVAL 1 WEEK))：获取周

```mysql
mysql> SELECT * FROM Student WHERE WEEK(Sage) = WEEK(DATE_ADD(CURDATE(), INTERVAL 1 WEEK));
+------+--------+---------------------+------+
| SId  | Sname  | Sage                | Ssex |
+------+--------+---------------------+------+
| 03   | 孙风   | 1990-05-20 00:00:00 | 男   |
+------+--------+---------------------+------+
1 row in set (0.00 sec)
```



## 题目3：查询本月过生日的学生

获取本月月份信息

```mysql
mysql> SELECT MONTH(NOW());
+--------------+
| MONTH(NOW()) |
+--------------+
|            5 |
+--------------+
1 row in set (0.00 sec)
```

获取本月份另外一个方法

```mysql
mysql> SELECT MONTH(CURDATE());
+------------------+
| MONTH(CURDATE()) |
+------------------+
|                5 |
+------------------+
1 row in set (0.00 sec)
```

条件过滤一下即可

```mysql
mysql> SELECT * FROM Student WHERE MONTH(Sage) = MONTH(CURDATE());
+------+--------+---------------------+------+
| SId  | Sname  | Sage                | Ssex |
+------+--------+---------------------+------+
| 03   | 孙风   | 1990-05-20 00:00:00 | 男   |
+------+--------+---------------------+------+
1 row in set (0.00 sec)
```



## 题目4：查询下月过生日的学生

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

# 总结

# 后记

其实没有固定的答案，结构更简单，思路更清晰，查询效率更快的方法，欢迎留言，我们一起学习，一起进步~~
