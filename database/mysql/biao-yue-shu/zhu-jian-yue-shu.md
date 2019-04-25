#### 主键约束 primary key

##### 主键作用：可以唯一表示一条数据，每张表里面只有一个主键。

##### 主键特性：非空且唯一，当表里没有主键的时，第一个出现的非空且为唯一的列，被当成主键。

注意：唯一标识一条数据

例子：

```
mysql> create table tb3(
    -> id int primary key,
    -> name varchar(20) not null
    -> );
Query OK, 0 rows affected (0.04 sec)

mysql> desc tb3;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int(11)     | NO   | PRI | NULL    |       |
| name  | varchar(20) | NO   |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
2 rows in set (0.00 sec)
```

##### 删除主键约束

```
mysql> alter table tb3
    -> drop primary key;
Query OK, 0 rows affected (0.10 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc tb3;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int(11)     | NO   |     | NULL    |       |
| name  | varchar(20) | NO   |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
2 rows in set (0.00 sec)
```

##### 添加主键约束

```
mysql> alter table tb3
    -> add primary key(id);
Query OK, 0 rows affected (0.11 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc tb3;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int(11)     | NO   | PRI | NULL    |       |
| name  | varchar(20) | NO   |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
2 rows in set (0.00 sec)
```



