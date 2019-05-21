[TOC]

# 题目
21. 查询任何一门课程成绩在 70 分以上的姓名、课程名称和分数



# 解释

```mysql
mysql> SELECT Student.Sname, Course.Cname, SC.score FROM Student, SC, Course WHERE SC.score >=70 AND Student.SId = SC.SId AND SC.CId = Course.CId; 
+--------+--------+-------+
| Sname  | Cname  | score |
+--------+--------+-------+
| 赵雷   | 语文   |  80.0 |
| 赵雷   | 数学   |  90.0 |
| 赵雷   | 英语   |  99.0 |
| 钱电   | 语文   |  70.0 |
| 钱电   | 英语   |  80.0 |
| 孙风   | 语文   |  80.0 |
| 孙风   | 数学   |  80.0 |
| 孙风   | 英语   |  80.0 |
| 周梅   | 语文   |  76.0 |
| 周梅   | 数学   |  87.0 |
| 郑竹   | 数学   |  89.0 |
| 郑竹   | 英语   |  98.0 |
+--------+--------+-------+
12 rows in set (0.00 sec)
```

# 总结
