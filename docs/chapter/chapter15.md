[TOC]

# 题目
1. 按各科成绩进行排序，并显示排名， Score 重复时保留名次空缺
2. 按各科成绩进行排序，并显示排名， Score 重复时合并名次



# 解释

## 题目1：按各科成绩进行排序，并显示排名， Score 重复时保留名次空缺

解题思路就是：使用两张成绩表，biao1用来做比较，biao2负责记录信息

例如：biao2中99分的同学，在表1中有0个，加上1就是他的排名了

```mysql
mysql> SELECT biao2.score, (SELECT COUNT( biao1.score ) + 1 FROM SC AS biao1 WHERE biao1.score > biao2.score) AS 排名 FROM SC AS biao2 ORDER BY biao2.score DESC;
+-------+--------+
| score | 排名   |
+-------+--------+
|  99.0 |      1 |
|  98.0 |      2 |
|  90.0 |      3 |
|  89.0 |      4 |
|  87.0 |      5 |
|  80.0 |      6 |
|  80.0 |      6 |
|  80.0 |      6 |
|  80.0 |      6 |
|  80.0 |      6 |
|  76.0 |     11 |
|  70.0 |     12 |
|  60.0 |     13 |
|  50.0 |     14 |
|  34.0 |     15 |
|  31.0 |     16 |
|  30.0 |     17 |
|  20.0 |     18 |
+-------+--------+
18 rows in set (0.00 sec)

```

## 题目2：按各科成绩进行排序，并显示排名， Score 重复时合并名次

首先，通过排序等到所有分数的人数

```mysql
mysql> SELECT score, count(score) FROM SC GROUP BY score ORDER BY score DESC;
+-------+--------------+
| score | count(score) |
+-------+--------------+
|  99.0 |            1 |
|  98.0 |            1 |
|  90.0 |            1 |
|  89.0 |            1 |
|  87.0 |            1 |
|  80.0 |            5 |
|  76.0 |            1 |
|  70.0 |            1 |
|  60.0 |            1 |
|  50.0 |            1 |
|  34.0 |            1 |
|  31.0 |            1 |
|  30.0 |            1 |
|  20.0 |            1 |
+-------+--------------+
14 rows in set (0.00 sec)
```

思想跟题目1就一样了，这次的biao1，就把所有80分的成绩聚合了

```mysql

mysql> SELECT biao2.score, ( SELECT count( biao1.score ) + 1  FROM ( SELECT score, count(score) FROM SC GROUP BY score ORDER BY score DESC ) AS biao1 WHERE biao1.score > biao2.score  ) AS rank1  FROM SC AS biao2  ORDER BY biao2.score DESC;
+-------+-------+
| score | rank1 |
+-------+-------+
|  99.0 |     1 |
|  98.0 |     2 |
|  90.0 |     3 |
|  89.0 |     4 |
|  87.0 |     5 |
|  80.0 |     6 |
|  80.0 |     6 |
|  80.0 |     6 |
|  80.0 |     6 |
|  80.0 |     6 |
|  76.0 |     7 |
|  70.0 |     8 |
|  60.0 |     9 |
|  50.0 |    10 |
|  34.0 |    11 |
|  31.0 |    12 |
|  30.0 |    13 |
|  20.0 |    14 |
+-------+-------+
18 rows in set (0.00 sec)
```

# 总结

看懂了，就非常简单了~~~

# 后记

其实没有固定的答案，结构更简单，思路更清晰，查询效率更快的方法，欢迎留言，我们一起学习，一起进步~~
