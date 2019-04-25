#### 一对一关系

##### 举例:学生表中有学号、姓名、学院，但学生还有些比如电话，家庭地址等比较私密的信息，这些信息不会放在学生表当中，会新建立一个学生详细信息表来存放。

##### 这时的学生表和学生详细信息表两者的关系就是一对一的关系，因为一个学生只能有一条详细信息。

##### 用主键加主键的方式来实现这种关系。

##### 建立学生表

```
mysql> create table student(
    -> id int primary key,
    -> name varchar(10) not null,
    -> college varchar(10) not null
    -> );
Query OK, 0 rows affected (0.07 sec)

mysql> desc student;
+---------+-------------+------+-----+---------+-------+
| Field   | Type        | Null | Key | Default | Extra |
+---------+-------------+------+-----+---------+-------+
| id      | int(11)     | NO   | PRI | NULL    |       |
| name    | varchar(10) | NO   |     | NULL    |       |
| college | varchar(10) | NO   |     | NULL    |       |
+---------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)
```

##### 建立学生详情表

```
mysql> create table student_details(
    -> id int primary key,
    -> sex varchar(20),
    -> age int
    -> );
Query OK, 0 rows affected (0.11 sec)

mysql> desc student_details;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int(11)     | NO   | PRI | NULL    |       |
| sex   | varchar(20) | YES  |     | NULL    |       |
| age   | int(11)     | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)
```

##### 为学生详情表添加一对一关系  （一对一：用外键的方式把两个表的主键关联）

    mysql> show create table student_details\G   ##查看student_details表是否有一对一关系如果没有就添加    
    *************************** 1. row ***************************
           Table: student_details
    Create Table: CREATE TABLE `student_details` (
      `id` int(11) NOT NULL,
      `sex` varchar(20) DEFAULT NULL,
      `age` int(11) DEFAULT NULL,
      PRIMARY KEY (`id`)
    ) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci
    1 row in set (0.00 sec)

    mysql> alter table student_details          ## 添加一对一关系方法
        -> add foreign key (id) references student(id);
    Query OK, 0 rows affected (0.09 sec)
    Records: 0  Duplicates: 0  Warnings: 0

    mysql> show create table student_details\G  ## 添加一对一关系后信息
    *************************** 1. row ***************************
           Table: student_details
    Create Table: CREATE TABLE `student_details` (
      `id` int(11) NOT NULL,
      `sex` varchar(20) DEFAULT NULL,
      `age` int(11) DEFAULT NULL,
      PRIMARY KEY (`id`),
      CONSTRAINT `student_details_ibfk_1` FOREIGN KEY (`id`) REFERENCES `student` (`id`)
    ) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci
    1 row in set (0.00 sec)

##### 为学生表插入数据

```
mysql> insert into student value(1,'rave','python'),(2,'leva','英语'),(3,'zlk','语文');
Query OK, 3 rows affected (0.02 sec)
Records: 3  Duplicates: 0  Warnings: 0

mysql> select * from student;
+----+------+---------+
| id | name | college |
+----+------+---------+
|  1 | rave | python  |
|  2 | leva | 英语    |
|  3 | zlk  | 语文    |
+----+------+---------+
3 rows in set (0.00 sec)
```

##### 为学生详情表插入数据

```
mysql> insert into student_details value(1,'男','18'),(2,'女','19'),(3,'男','20');
Query OK, 2 rows affected (0.05 sec)
Records: 2  Duplicates: 0  Warnings: 0

mysql> select * from student_details;
+----+------+------+
| id | sex  | age  |
+----+------+------+
|  1 | 男   |   18 |
|  2 | 女   |   19 |
|  3 | 男   |   20 |
+----+------+------+
3 rows in set (0.00 sec)
```



