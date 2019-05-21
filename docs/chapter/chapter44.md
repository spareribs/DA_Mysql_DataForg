[TOC]

# 题目
21. 查询本月过生日的学生


# 解释

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

过滤即可

```mysql
mysql> SELECT * FROM Student WHERE MONTH(Sage) = MONTH(CURDATE());
+------+--------+---------------------+------+
| SId  | Sname  | Sage                | Ssex |
+------+--------+---------------------+------+
| 03   | 孙风   | 1990-05-20 00:00:00 | 男   |
+------+--------+---------------------+------+
1 row in set (0.00 sec)
```

参考答案

```mysql
select *
from student 
where EXTRACT(YEAR_MONTH FROM student.Sage)=EXTRACT(YEAR_MONTH FROM CURDATE())
```



# 总结

