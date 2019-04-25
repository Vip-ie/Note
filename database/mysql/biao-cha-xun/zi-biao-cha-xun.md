#### 子查询

求出学生的平均年龄

```
mysql> select avg(age) from sst;
+----------+
| avg(age) |
+----------+
|  20.0000 |
+----------+
1 row in set (0.00 sec)

mysql> select * from sst;
+----+------+-----+
| id | name | age |
+----+------+-----+
|  1 | zlk  |  18 |
|  2 | rave |  20 |
|  3 | leva |  22 |
+----+------+-----+
3 rows in set (0.00 sec)
```

查找出大于平均年龄的数据

```
mysql> select * from sst;
+----+------+-----+
| id | name | age |
+----+------+-----+
|  1 | zlk  |  18 |
|  2 | rave |  20 |
|  3 | leva |  22 |
+----+------+-----+
3 rows in set (0.00 sec)

mysql> select * from sst where age > 18.25;
+----+------+-----+
| id | name | age |
+----+------+-----+
|  2 | rave |  20 |
|  3 | leva |  22 |
+----+------+-----+
2 rows in set (0.00 sec)
```

将平均数的sql语句作为子查询放入上一条语句中

```
mysql> select * from sst where age > (select avg(age) from sst);
+----+------+-----+
| id | name | age |
+----+------+-----+
|  3 | leva |  22 |
+----+------+-----+
1 row in set (0.00 sec)

mysql> select * from sst;
+----+------+-----+
| id | name | age |
+----+------+-----+
|  1 | zlk  |  18 |
|  2 | rave |  20 |
|  3 | leva |  22 |
+----+------+-----+
3 rows in set (0.00 sec)
```

需求：要查找，软件和语言 的学生人数

in表示两条以上数据使用

```
mysql> select * from student where ts_id in(
    -> select tz_id from tanzhou where tz_name='软件' or tz_name='语言');
+------+-----------+-------+
| s_id | s_name    | ts_id |
+------+-----------+-------+
|    4 | 班长      |     1 |
|    5 | lucky     |     1 |
|    7 | jiangeng  |     1 |
|    2 | 玲玲      |     2 |
|    9 | 张力凯    |     2 |
+------+-----------+-------+
5 rows in set (0.00 sec)
```



