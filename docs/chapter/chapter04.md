[TOC]

# 题目
1. 查询所有同学的学生编号、学生姓名、选课总数、所有课程的总成绩(没成绩的显示为null)  
2.  查有成绩的学生信息



# 解释

## 题4.1：查询所有同学的学生编号、学生姓名、选课总数、所有课程的总成绩(没成绩的显示为null)  

```mysql
mysql> SELECT SId,Count(SId),SUM(Score) FROM SC GROUP BY SId;   
+------+------------+------------+
| SId  | Count(SId) | SUM(Score) |
+------+------------+------------+
| 01   |          3 |      269.0 |
| 02   |          3 |      210.0 |
| 03   |          3 |      240.0 |
| 04   |          3 |      100.0 |
| 05   |          2 |      163.0 |
| 06   |          2 |       65.0 |
| 07   |          2 |      187.0 |
+------+------------+------------+
7 rows in set (0.00 sec)

```



```mysql
mysql> SELECT biao1.SId, biao1.Sname, biao2.countcourse, biao2.sumscore FROM Student AS biao1 LEFT JOIN (SELECT SId, Count(CId) AS countcourse, SUM(Score) AS sumscore FROM SC GROUP BY SId) AS biao2 ON biao1.SId=biao2.SId;   
+------+--------+-------------+----------+
| SId  | Sname  | countcourse | sumscore |
+------+--------+-------------+----------+
| 01   | 赵雷   |           3 |    269.0 |
| 02   | 钱电   |           3 |    210.0 |
| 03   | 孙风   |           3 |    240.0 |
| 04   | 李云   |           3 |    100.0 |
| 05   | 周梅   |           2 |    163.0 |
| 06   | 吴兰   |           2 |     65.0 |
| 07   | 郑竹   |           2 |    187.0 |
| 09   | 张三   |        NULL |     NULL |
| 10   | 李四   |        NULL |     NULL |
| 11   | 李四   |        NULL |     NULL |
| 12   | 赵六   |        NULL |     NULL |
| 13   | 孙七   |        NULL |     NULL |
+------+--------+-------------+----------+
12 rows in set (0.00 sec)
```

## 题4.2：查有成绩的学生信息

```mysql
mysql> SELECT * FROM Student WHERE EXISTS(SELECT * FROM SC WHERE Student.SId=SC.SId);
+------+--------+---------------------+------+
| SId  | Sname  | Sage                | Ssex |
+------+--------+---------------------+------+
| 01   | 赵雷   | 1990-01-01 00:00:00 | 男   |
| 02   | 钱电   | 1990-12-21 00:00:00 | 男   |
| 03   | 孙风   | 1990-05-20 00:00:00 | 男   |
| 04   | 李云   | 1990-08-06 00:00:00 | 男   |
| 05   | 周梅   | 1991-12-01 00:00:00 | 女   |
| 06   | 吴兰   | 1992-03-01 00:00:00 | 女   |
| 07   | 郑竹   | 1989-07-01 00:00:00 | 女   |
+------+--------+---------------------+------+
7 rows in set (0.00 sec)
```



# 总结