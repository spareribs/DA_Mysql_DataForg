[TOC]

# 题目
1. 查询各科成绩最高分、最低分和平均分： 以如下形式显示：课程 ID，课程 name，最高分，最低分，平均分，及格率，中等率，优良率，优秀率 及格为>=60，中等为：70-80，优良为：80-90，优秀为：>=90 要求输出课程号和选修人数，查询结果按人数降序排列，若人数相同，按课程号升序排列



# 解释

首先，是计算出所有的：最高分，最低分，平均分，选修人数

```mysql
mysql> SELECT CId, MAX(score) AS 最高分 , MIN(score) AS 最低分, AVG(score) AS 平均分, COUNT(*) AS 选修人数 FROM SC GROUP BY CId;
+------+-----------+-----------+-----------+--------------+
| CId  | 最高分    | 最低分    | 平均分    | 选修人数     |
+------+-----------+-----------+-----------+--------------+
| 01   |      80.0 |      31.0 |  64.50000 |            6 |
| 02   |      90.0 |      30.0 |  72.66667 |            6 |
| 03   |      99.0 |      20.0 |  68.50000 |            6 |
+------+-----------+-----------+-----------+--------------+
3 rows in set (0.00 sec)
```

然后，对结果进行排序

```mysql
mysql> SELECT CId, MAX(score) AS 最高分 , MIN(score) AS 最低分, AVG(score) AS 平均分, COUNT(*) AS 选修人数 FROM SC GROUP BY CId ORDER BY COUNT(*) DESC, SC.CId ASC;
+------+-----------+-----------+-----------+--------------+
| CId  | 最高分    | 最低分    | 平均分    | 选修人数     |
+------+-----------+-----------+-----------+--------------+
| 01   |      80.0 |      31.0 |  64.50000 |            6 |
| 02   |      90.0 |      30.0 |  72.66667 |            6 |
| 03   |      99.0 |      20.0 |  68.50000 |            6 |
+------+-----------+-----------+-----------+--------------+
3 rows in set (0.00 sec)
```

这里主要用到 CASE WHEN THEN ELSE END的方法

```mysql
mysql> SELECT CId, MAX(score) AS 最高分 , MIN(score) AS 最低分, AVG(score) AS 平均分, COUNT(*) AS 选修人数, SUM(CASE WHEN SC.score >= 60 then 1 else 0 end )/COUNT(*) AS 及格率, SUM(CASE WHEN SC.score >= 70 AND SC.score < 80 THEN 1 ELSE 0 END )/COUNT(*) AS 中等率, SUM(CASE WHEN SC.score >=80 AND SC.score < 90 THEN 1 ELSE 0 END )/COUNT(*) AS 优良率, SUM(CASE WHEN SC.score >= 90 THEN 1 ELSE 0 END )/COUNT(*) AS 优秀率 FROM SC GROUP BY CId ORDER BY COUNT(*) DESC, SC.CId ASC;
+------+-----------+-----------+-----------+--------------+-----------+-----------+-----------+-----------+
| CId  | 最高分    | 最低分    | 平均分    | 选修人数     | 及格率    | 中等率    | 优良率    | 优秀率    |
+------+-----------+-----------+-----------+--------------+-----------+-----------+-----------+-----------+
| 01   |      80.0 |      31.0 |  64.50000 |            6 |    0.6667 |    0.3333 |    0.3333 |    0.0000 |
| 02   |      90.0 |      30.0 |  72.66667 |            6 |    0.8333 |    0.0000 |    0.5000 |    0.1667 |
| 03   |      99.0 |      20.0 |  68.50000 |            6 |    0.6667 |    0.0000 |    0.3333 |    0.3333 |
+------+-----------+-----------+-----------+--------------+-----------+-----------+-----------+-----------+
3 rows in set (0.00 sec)
```

# 总结

新出现的方法： CASE WHEN THEN ELSE END

# 后记

其实没有固定的答案，结构更简单，思路更清晰，查询效率更快的方法，欢迎留言，我们一起学习，一起进步~~