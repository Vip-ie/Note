#### MySQL 创建表

##### 创建表 语法

```
create table [if not exists] table_name(
                                        column_name data_type,
                                        );
```

##### 

```
mysql> create table if not exists student(
    -> id int,
    -> name varchar(10)
    -> );
Query OK, 0 rows affected (0.06 sec)
```

#### 查看数据表结构 语法

##### describe tb\_name;

```
mysql> desc student;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int(11)     | YES  |     | NULL    |       |
| name  | varchar(10) | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
2 rows in set (0.00 sec)
```

##### show create table tb\_name;\(\G\)查看表结构使用了那些命令

    mysql> show create table student\G
    *************************** 1. row ***************************
           Table: student
    Create Table: CREATE TABLE `student` (
      `id` int(11) DEFAULT NULL,
      `name` varchar(10) DEFAULT NULL
    ) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci
    1 row in set (0.00 sec)

#### 查看数据库里有那些表 语法

##### show tables;

```
mysql> show tables;
+----------------+
| Tables_in_test |
+----------------+
| student        |
+----------------+
1 row in set (0.00 sec)
```

#### 删除表 语法

#### drop table tablename;

```
mysql> drop table student;
Query OK, 0 rows affected (0.03 sec)
```



