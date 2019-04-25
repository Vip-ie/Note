#### 多对多关系

举例：学生要报名选修课，一个学生可以报多门课程，一个课程有很多的学生报名，那么学生表与课程表两者就形成了多堆多关系。

##### 对于多对多关系，需要创建中间表实现

##### 建立课程表

```
mysql> create table cours(
    -> id int primary key auto_increment,  ##课程表ID
    -> name varchar(20) not null           ##课程表名称
    -> );
Query OK, 0 rows affected (0.05 sec)

mysql> desc cours;
+-------+-------------+------+-----+---------+----------------+
| Field | Type        | Null | Key | Default | Extra          |
+-------+-------------+------+-----+---------+----------------+
| id    | int(11)     | NO   | PRI | NULL    | auto_increment |
| name  | varchar(20) | NO   |     | NULL    |                |
+-------+-------------+------+-----+---------+----------------+
2 rows in set (0.00 sec)
```

##### 为课程表插入数据

```
mysql> insert into cours values(1,'python'),(2,'englise'),(3,'java');
Query OK, 3 rows affected (0.07 sec)
Records: 3  Duplicates: 0  Warnings: 0

mysql> select * from cours;
+----+---------+
| id | name    |
+----+---------+
|  1 | python  |
|  2 | englise |
|  3 | java    |
+----+---------+
3 rows in set (0.00 sec)
```

##### 建立选课表（中间表）

    mysql> create table zj(
        -> id_s int,                                  ##学生ID
        -> id_c int,                                  ##课程ID
        -> primary key(id_s,id_c),                    ##联合主键，防止重复出现，唯一的
        -> foreign key(id_s) references student(id),  ##关联学生表
        -> foreign key(id_c) references cours(id)     ##关联课程表
        -> );
    Query OK, 0 rows affected (0.07 sec)

    mysql> desc zj;
    +-------+---------+------+-----+---------+-------+
    | Field | Type    | Null | Key | Default | Extra |
    +-------+---------+------+-----+---------+-------+
    | id_s  | int(11) | NO   | PRI | NULL    |       |
    | id_c  | int(11) | NO   | PRI | NULL    |       |
    +-------+---------+------+-----+---------+-------+
    2 rows in set (0.01 sec)

    mysql> show create table zj\G
    *************************** 1. row ***************************
           Table: zj
    Create Table: CREATE TABLE `zj` (
      `id_s` int(11) NOT NULL,
      `id_c` int(11) NOT NULL,
      PRIMARY KEY (`id_s`,`id_c`),
      KEY `id_c` (`id_c`),
      CONSTRAINT `zj_ibfk_1` FOREIGN KEY (`id_s`) REFERENCES `student` (`id`),
      CONSTRAINT `zj_ibfk_2` FOREIGN KEY (`id_c`) REFERENCES `cours` (`id`)
    ) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci
    1 row in set (0.00 sec)

##### 中间表选课方法

```
mysql> insert into zj value(2,3);
Query OK, 1 row affected (0.05 sec)

mysql> select * from zj;
+------+------+
| id_s | id_c |
+------+------+
|    2 |    3 |
+------+------+
1 row in set (0.00 sec)
```

##### 建立学生表

```
mysql> create table student(
    -> id int primary key auto_increment,  ##学生ID
    -> name varchar(10)                    ##学生名字
    -> );
Query OK, 0 rows affected (0.06 sec)

mysql> desc student;
+-------+-------------+------+-----+---------+----------------+
| Field | Type        | Null | Key | Default | Extra          |
+-------+-------------+------+-----+---------+----------------+
| id    | int(11)     | NO   | PRI | NULL    | auto_increment |
| name  | varchar(10) | YES  |     | NULL    |                |
+-------+-------------+------+-----+---------+----------------+
2 rows in set (0.00 sec)
```

##### 为学生表插入数据

```
mysql> insert into student values(1,'rvae',2),(2,'leva',1),(3,'zlk');
Query OK, 3 rows affected (0.07 sec)
Records: 3  Duplicates: 0  Warnings: 0

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



