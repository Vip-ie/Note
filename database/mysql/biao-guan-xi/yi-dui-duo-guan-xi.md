#### 一对多关系

##### 举例，通常情况下，学校中一个学院可以有很多的学生，而一个学生只属于某一个学院。

##### 学院与学生之间的关系就是一对多的关系，通过外键联系来实现这种关系

##### 创建学院表

```
mysql> create table department(
    -> id int primary key auto_increment,   ##学院ID
    -> name varchar(20)                     ##学院名
    -> );
Query OK, 0 rows affected (0.09 sec)

mysql> desc department;
+-------+-------------+------+-----+---------+----------------+
| Field | Type        | Null | Key | Default | Extra          |
+-------+-------------+------+-----+---------+----------------+
| id    | int(11)     | NO   | PRI | NULL    | auto_increment |
| name  | varchar(20) | YES  |     | NULL    |                |
+-------+-------------+------+-----+---------+----------------+
2 rows in set (0.00 sec)
```

##### 创建学生表（学生表中，只能添加已有的学院ID）

```
mysql> create table student(
    -> id int primary key auto_increment,  ##学生ID
    -> name varchar(20) not null,          ##学生名字
    -> dept_id int not null                ##所属学院ID
    -> );
Query OK, 0 rows affected (0.11 sec)

mysql> desc student;
+---------+-------------+------+-----+---------+----------------+
| Field   | Type        | Null | Key | Default | Extra          |
+---------+-------------+------+-----+---------+----------------+
| id      | int(11)     | NO   | PRI | NULL    | auto_increment |
| name    | varchar(20) | NO   |     | NULL    |                |
| dept_id | int(11)     | NO   |     | NULL    |                |
+---------+-------------+------+-----+---------+----------------+
3 rows in set (0.01 sec)
```

##### 建立一对多关系

    mysql> alter table student
        -> add foreign key (dept_id) references department(id);
    Query OK, 0 rows affected (0.03 sec)
    Records: 0  Duplicates: 0  Warnings: 0

    mysql> show create table student\G
    *************************** 1. row ***************************
           Table: student
    Create Table: CREATE TABLE `student` (
      `id` int(11) NOT NULL AUTO_INCREMENT,
      `name` varchar(20) NOT NULL,
      `dept_id` int(11) NOT NULL,
      PRIMARY KEY (`id`),
      KEY `dept_id` (`dept_id`),
      CONSTRAINT `student_ibfk_1` FOREIGN KEY (`dept_id`) REFERENCES `department` (`id`)
    ) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci
    1 row in set (0.01 sec)

##### 删除一对多关系

    mysql> show create table student\G
    *************************** 1. row ***************************
           Table: student
    Create Table: CREATE TABLE `student` (
      `id` int(11) NOT NULL AUTO_INCREMENT,
      `name` varchar(20) NOT NULL,
      `dept_id` int(11) NOT NULL,
      PRIMARY KEY (`id`),
      KEY `dept_id` (`dept_id`),
      CONSTRAINT `student_ibfk_1` FOREIGN KEY (`dept_id`) REFERENCES `department` (`id`)
    ) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci
    1 row in set (0.01 sec)

    mysql> alter table student drop foreign key student_ibfk_1;
    Query OK, 0 rows affected (0.08 sec)
    Records: 0  Duplicates: 0  Warnings: 0

##### 学院表插入数据

```
mysql> insert into department values(1,'外语学院'),(2,'计算机学院');
Query OK, 2 rows affected (0.07 sec)
Records: 2  Duplicates: 0  Warnings: 0

mysql> select * from department;
+----+-----------------+
| id | name            |
+----+-----------------+
|  1 | 外语学院        |
|  2 | 计算机学院      |
+----+-----------------+
2 rows in set (0.00 sec)
```

##### 学生表插入数据

```
mysql> insert into student values(1,'佳能',2),(2,'leva',1);
Query OK, 2 rows affected (0.01 sec)
Records: 2  Duplicates: 0  Warnings: 0

mysql> select * from student;
+----+--------+---------+
| id | name   | dept_id |
+----+--------+---------+
|  1 | 佳能   |       2 |
|  2 | leva   |       1 |
+----+--------+---------+
2 rows in set (0.00 sec)
```



