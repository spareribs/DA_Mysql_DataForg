[TOC]

# 题目
1. 查询不同课程成绩相同的学生的学生编号、课程编号、学生成绩





# 解释

先把2个成绩表做笛卡尔积，然后通过条件判断把需要的学习信息提取出来

```mysql
mysql> SELECT biao1.*, biao2.* FROM SC AS biao1, SC AS biao2 WHERE biao1.CId != biao2.CId AND biao1.SId != biao2.SId AND biao1.score=biao2.score;
+------+------+-------+------+------+-------+
| SId  | CId  | score | SId  | CId  | score |
+------+------+-------+------+------+-------+
| 02   | 03   |  80.0 | 01   | 01   |  80.0 |
| 03   | 02   |  80.0 | 01   | 01   |  80.0 |
| 03   | 03   |  80.0 | 01   | 01   |  80.0 |
| 01   | 01   |  80.0 | 02   | 03   |  80.0 |
| 03   | 01   |  80.0 | 02   | 03   |  80.0 |
| 03   | 02   |  80.0 | 02   | 03   |  80.0 |
| 02   | 03   |  80.0 | 03   | 01   |  80.0 |
| 01   | 01   |  80.0 | 03   | 02   |  80.0 |
| 02   | 03   |  80.0 | 03   | 02   |  80.0 |
| 01   | 01   |  80.0 | 03   | 03   |  80.0 |
+------+------+-------+------+------+-------+
10 rows in set (0.00 sec)
```

直接使用去重把结果筛选出来

```mysql
mysql> SELECT DISTINCT biao1.*  FROM SC AS biao1, SC AS biao2 WHERE biao1.CId != biao2.CId AND biao1.SId != biao2.SId AND biao1.score=biao2.score; 
+------+------+-------+
| SId  | CId  | score |
+------+------+-------+
| 02   | 03   |  80.0 |
| 03   | 02   |  80.0 |
| 03   | 03   |  80.0 |
| 01   | 01   |  80.0 |
| 03   | 01   |  80.0 |
+------+------+-------+
5 rows in set (0.00 sec)
```



# 总结
