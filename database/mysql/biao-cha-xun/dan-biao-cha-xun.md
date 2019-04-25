#### 单表查询

##### 1. 查询所有记录

```
mysql> select * from student;
+----+------+
| id | name |
+----+------+
|  1 | rvae |
|  2 | leva |
|  3 | zlk  |
+----+------+
3 rows in set (0.00 sec)
```

##### 2. 查询选中列记录

```
mysql> select id from student;
+----+
| id |
+----+
|  1 |
|  2 |
|  3 |
+----+
3 rows in set (0.00 sec)
```

##### 3. 查询指定条件下的记录

```
mysql> select id from student where id>2;
+----+
| id |
+----+
|  3 |
+----+
1 row in set (0.00 sec)
```

##### 4. 查询后为列取别名

```
mysql> select name as 姓名 from student;
+--------+
| 姓名   |
+--------+
| rvae   |
| leva   |
| zlk    |
+--------+
3 rows in set (0.00 sec)
```

##### 5. 模糊查询

```
mysql> select * from student where name like 'z%';    ##z%  %表示所有所有数据
+----+------+
| id | name |
+----+------+
|  3 | zlk  |
+----+------+
1 row in set (0.00 sec)
```

```
mysql> select * from student where name like 'z_ _';  ## z _表示一个字符  _ _表示两个字符以此类推。
+----+------+
| id | name |
+----+------+
|  3 | zlk  |
+----+------+
1 row in set (0.00 sec)
```

##### 6. 排序ordery by

asc升序（默认）

```
mysql> select * from student order by id asc;
+----+------+
| id | name |
+----+------+
|  1 | rvae |
|  2 | leva |
|  3 | zlk  |
+----+------+
3 rows in set (0.00 sec)
```

desc（降序）

```
mysql> select * from student order by id desc;;
+----+------+
| id | name |
+----+------+
|  3 | zlk  |
|  2 | leva |
|  1 | rvae |
+----+------+
3 rows in set (0.00 sec)
```

##### 7. 限制显示数据的数量limit

按学生学号升序输出的前2条数据

```
mysql> select * from student order by id limit 2; 
+----+------+
| id | name |
+----+------+
|  1 | rvae |
|  2 | leva |
+----+------+
2 rows in set (0.00 sec)
```

指定的返回的数据的位置和数量

```
mysql> select * from zj order by id_s limit 2,2;
+------+------+
| id_s | id_c |
+------+------+
|    2 |    1 |
|    2 |    2 |
+------+------+
2 rows in set (0.00 sec)hiding
```

##### 8. 常用聚合函数

求最大年龄 max

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

mysql> select max(age) from sst;
+----------+
| max(age) |
+----------+
|       22 |
+----------+
1 row in set (0.00 sec)
```

求最小年龄 min

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

mysql> select min(age) from sst;
+----------+
| min(age) |
+----------+
|       18 |
+----------+
1 row in set (0.00 sec)
```

求和 sum

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


mysql> select  sum(age) from sst;
+----------+
| sum(age) |
+----------+
|       60 |
+----------+
1 row in set (0.00 sec)
```

求平均数 avg

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

mysql> select avg(age) from sst;
+----------+
| avg(age) |
+----------+
|  20.0000 |
+----------+
1 row in set (0.00 sec)
```

四舍五入 found

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

mysql> select round(avg(age)) from sst;
+-----------------+
| round(avg(age)) |
+-----------------+
|              20 |
+-----------------+
1 row in set (0.01 sec)
```

统计 count

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

mysql> select count(id) from sst;
+-----------+
| count(id) |
+-----------+
|         3 |
+-----------+
1 row in set (0.00 sec)
```

##### 9. 分组查询 group by

```
分组表
mysql> select * from student;
+------+-----------+-------+
| s_id | s_name    | ts_id |
+------+-----------+-------+
|    1 | 三花      |     3 |
|    2 | 玲玲      |     2 |
|    3 | 林林      |     4 |
|    4 | 班长      |     1 |
|    5 | lucky    |     1 |
|    6 | 王为      |     4 |
|    7 | jiangeng |     1 |
|    8 | 三花花    |     3 |
|    9 | 张力凯    |     2 |
+------+-----------+-------+
9 rows in set (0.00 sec)

分组方法一
mysql> select count(ts_id) from student group by ts_id;
+--------------+
| count(ts_id) |
+--------------+
|            3 |
|            2 |
|            2 |
|            2 |
+--------------+
4 rows in set (0.00 sec)

分组方法二
mysql> select ts_id,  count(ts_id) from student group by ts_id;
+-------+--------------+
| ts_id | count(ts_id) |
+-------+--------------+
|     1 |            3 |
|     2 |            2 |
|     3 |            2 |
|     4 |            2 |
+-------+--------------+
4 rows in set (0.00 sec)

分组查询指定某一条件方法
mysql> select ts_id,  count(ts_id) from student group by ts_id having count(ts_id)=3;
+-------+--------------+
| ts_id | count(ts_id) |
+-------+--------------+
|     1 |            3 |
+-------+--------------+
1 row in set (0.00 sec)
```



