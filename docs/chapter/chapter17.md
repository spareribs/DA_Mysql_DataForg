[TOC]

# 题目
1. 统计各科成绩各分数段人数：课程编号，课程名称，[100-85]，[85-70]，[70-60]，[60-0] 及所占百分比



# 解释

这一题跟14题很像，多了一个左链接，可以回去翻阅14题的流程

```mysql
mysql> SELECT Course.CId, Course.Cname, biao1.`[100-85]`, biao1.`(85-70]`, biao1.`(70-60]`, biao1.`(60-0]`  FROM ( SELECT CId, SUM( CASE WHEN SC.score >= 85 AND SC.score < 100 THEN 1 ELSE 0 END ) / COUNT( * ) AS `[100-85]`, SUM( CASE WHEN SC.score >= 70 AND SC.score < 85 THEN 1 ELSE 0 END ) / COUNT( * ) AS `(85-70]`, SUM( CASE WHEN SC.score < 70 AND SC.score >= 60 THEN 1 ELSE 0 END ) / COUNT( * ) AS `(70-60]`, SUM( CASE WHEN SC.score < 60 THEN 1 ELSE 0 END ) / COUNT( * ) AS `(60-0]`  FROM SC  GROUP BY CId  ORDER BY COUNT( * ) DESC, SC.CId ASC  ) AS biao1 LEFT JOIN Course ON Course.CId = biao1.CId;
+------+--------+----------+---------+---------+--------+
| CId  | Cname  | [100-85] | (85-70] | (70-60] | (60-0] |
+------+--------+----------+---------+---------+--------+
| 01   | 语文   |   0.0000 |  0.6667 |  0.0000 | 0.3333 |
| 02   | 数学   |   0.5000 |  0.1667 |  0.1667 | 0.1667 |
| 03   | 英语   |   0.3333 |  0.3333 |  0.0000 | 0.3333 |
+------+--------+----------+---------+---------+--------+
3 rows in set (0.00 sec)
```

这里还需要多一个100%

```mysql
mysql> SELECT Course.CId, Course.Cname, biao1.`[100-85]`, biao1.`(85-70]`, biao1.`(70-60]`, biao1.`(60-0]`  FROM ( SELECT CId, CONCAT(SUM( CASE WHEN SC.score >= 85 AND SC.score < 100 THEN 1 ELSE 0 END ) / COUNT( * )*100,'%') AS `[100-85]`, CONCAT(SUM( CASE WHEN SC.score >= 70 AND SC.score < 85 THEN 1 ELSE 0 END ) / COUNT( * )*100,'%') AS `(85-70]`, CONCAT(SUM( CASE WHEN SC.score < 70 AND SC.score >= 60 THEN 1 ELSE 0 END ) / COUNT( * )*100,'%') AS `(70-60]`, CONCAT(SUM( CASE WHEN SC.score < 60 THEN 1 ELSE 0 END ) / COUNT( * )*100,'%') AS `(60-0]`  FROM SC  GROUP BY CId  ORDER BY COUNT( * ) DESC, SC.CId ASC  ) AS biao1 LEFT JOIN Course ON Course.CId = biao1.CId;
+------+--------+----------+----------+----------+----------+
| CId  | Cname  | [100-85] | (85-70]  | (70-60]  | (60-0]   |
+------+--------+----------+----------+----------+----------+
| 01   | 语文   | 0.0000%  | 66.6667% | 0.0000%  | 33.3333% |
| 02   | 数学   | 50.0000% | 16.6667% | 16.6667% | 16.6667% |
| 03   | 英语   | 33.3333% | 33.3333% | 0.0000%  | 33.3333% |
+------+--------+----------+----------+----------+----------+
3 rows in set (0.00 sec)
```



# 总结

# 后记

其实没有固定的答案，结构更简单，思路更清晰，查询效率更快的方法，欢迎留言，我们一起学习，一起进步~~
