练习题

1. 建一张学生表包含（id、姓名、年龄、性别）。

```
mysql> create table student(
    -> id int,
    -> name varchar(10),
    -> age int,
    -> sex varchar(10)
    -> );
Query OK, 0 rows affected (0.09 sec)
```

1. 查看表结构

```
mysql> desc student;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int(11)     | YES  |     | NULL    |       |
| name  | varchar(10) | YES  |     | NULL    |       |
| age   | int(11)     | YES  |     | NULL    |       |
| sex   | varchar(10) | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
4 rows in set (0.00 sec)
```

1. 增加四条数据

```
mysql> insert into student values(1,'zlk',25,'男'),(2,'rave',23,'女'),(3,'leva',29,'女'),(4,'one',25,'女');
Query OK, 4 rows affected (0.03 sec)
Records: 4  Duplicates: 0  Warnings: 0
```

1. 查询所有数据

```
mysql> select * from student;
+------+------+------+------+
| id   | name | age  | sex  |
+------+------+------+------+
|    1 | zlk  |   25 | 男   |
|    2 | rave |   23 | 女   |
|    3 | leva |   29 | 女   |
|    4 | one  |   25 | 女   |
+------+------+------+------+
4 rows in set (0.00 sec)
```

1. 删除id=3的数据

```
mysql> delete from student where id = 3;
Query OK, 1 row affected (0.09 sec)mysql> 

mysql>select * from student;
+------+------+------+------+
| id   | name | age  | sex  |
+------+------+------+------+
|    1 | zlk  |   25 | 男   |
|    2 | rave |   23 | 女   |
|    4 | one  |   25 | 女   |
+------+------+------+------+
3 rows in set (0.00 sec)
```

1. 将性别女的，修改为男

```
mysql> update student set sex = '男' where id = 2;
Query OK, 1 row affected (0.10 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> update student set sex = '男' where id = 4;
Query OK, 0 rows affected (0.00 sec)
Rows matched: 0  Changed: 0  Warnings: 0

mysql> select * from student;
+------+------+------+------+
| id   | name | age  | sex  |
+------+------+------+------+
|    1 | zlk  |   25 | 男   |
|    2 | rave |   23 | 男   |
|    4 | one  |   25 | 男   |
+------+------+------+------+
3 rows in set (0.01 sec)
```

1. 简单说明用户，数据库，表与数据的关系。

```

```



