[TOC]

# 题目
1. 查询学生的总成绩，并进行排名，总分重复时保留名次空缺
2. 查询学生的总成绩，并进行排名，总分重复时不保留名次空缺



# 解释

与15题类似，只是分数改成总分了，这个相当于原始表

```mysql
mysql> SELECT SID, SUM(score) FROM SC GROUP BY SId;
+------+------------+
| SID  | SUM(score) |
+------+------------+
| 01   |      269.0 |
| 02   |      210.0 |
| 03   |      240.0 |
| 04   |      100.0 |
| 05   |      163.0 |
| 06   |       65.0 |
| 07   |      187.0 |
+------+------------+
7 rows in set (0.00 sec)
```

## 题目1：查询学生的总成绩，并进行排名，总分重复时保留名次空缺

```mysql
mysql> SELECT biao2.scoresum, (SELECT COUNT( biao1.scoresum ) + 1 FROM (SELECT SId, SUM(score) AS scoresum FROM SC GROUP BY SId)  AS biao1 WHERE biao1.scoresum > biao2.scoresum) AS 排名 FROM (SELECT SId, SUM(score) AS scoresum FROM SC GROUP BY SId) AS biao2 ORDER BY biao2.scoresum DESC;
+----------+--------+
| scoresum | 排名   |
+----------+--------+
|    269.0 |      1 |
|    240.0 |      2 |
|    210.0 |      3 |
|    187.0 |      4 |
|    163.0 |      5 |
|    100.0 |      6 |
|     65.0 |      7 |
+----------+--------+
7 rows in set (0.00 sec)
```

## 题目2：查询学生的总成绩，并进行排名，总分重复时不保留名次空缺

```mysql

mysql> SELECT biao2.scoresum, ( SELECT count( biao1.scoresum ) + 1  FROM ( SELECT scoresum, count( scoresum )  FROM ( SELECT SId, SUM( score ) AS scoresum FROM SC GROUP BY SId ) AS biao0  GROUP BY biao0.scoresum  ORDER BY biao0.scoresum DESC  ) AS biao1  WHERE biao1.scoresum > biao2.scoresum  ) AS rank1  FROM ( SELECT SId, SUM( score ) AS scoresum FROM SC GROUP BY SId ) AS biao2  ORDER BY biao2.scoresum DESC;
+----------+-------+
| scoresum | rank1 |
+----------+-------+
|    269.0 |     1 |
|    240.0 |     2 |
|    210.0 |     3 |
|    187.0 |     4 |
|    163.0 |     5 |
|    100.0 |     6 |
|     65.0 |     7 |
+----------+-------+
7 rows in set (0.00 sec)
```



# 总结

# 后记

其实没有固定的答案，结构更简单，思路更清晰，查询效率更快的方法，欢迎留言，我们一起学习，一起进步~~