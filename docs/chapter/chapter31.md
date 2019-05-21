[TOC]

# 题目
1. 查询课程编号为 01 且课程成绩在 80 分以上的学生的学号和姓名

# 解释

```mysql
mysql> SELECT DISTINCT Student.SId, Student.Sname FROM Student, SC WHERE SC.score >=80 AND Student.SId = SC.SId AND SC.CId="01";   
+------+--------+
| SId  | Sname  |
+------+--------+
| 01   | 赵雷   |
| 03   | 孙风   |
+------+--------+
2 rows in set (0.00 sec)

```



# 总结

