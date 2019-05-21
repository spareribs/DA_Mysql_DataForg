[TOC]

# 题目
1. 查询下周过生日的学生



# 解释

当前时间

```mysql
mysql> SELECT NOW();
+---------------------+
| NOW()               |
+---------------------+
| 2019-05-16 13:13:38 |
+---------------------+
1 row in set (0.00 sec)
```

下周生日的小伙伴

```mysql
mysql> SELECT * FROM Student WHERE WEEK(Sage) = WEEK(DATE_ADD(CURDATE(), INTERVAL 1 WEEK));
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
where YEARWEEK(student.Sage)=CONCAT(YEAR(CURDATE()),week(CURDATE())+1)
```



# 总结

