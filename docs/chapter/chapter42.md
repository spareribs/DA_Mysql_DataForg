[TOC]

# 题目
1. 查询本周过生日的学生





# 解释

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

参考答案：

```mysql
select *
from student 
where YEARWEEK(student.Sage)=YEARWEEK(CURDATE())
```

```mysql

```

```mysql

```

```mysql

```

```mysql

```



# 总结

