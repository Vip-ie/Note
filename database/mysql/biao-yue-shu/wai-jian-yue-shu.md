#### 外键约束 foreign key

##### 外键约束：保持数据一致性，完整性实现一对多关系。

##### 外键必须关联到键上面去，一般情况，关联到另一张表的主键。

（因为一个表只存一类信息。用外键来做参照，保证数据的一致性，可以减少数据冗余）

表A （A表中a\_id被参照数据，不能被修改和删除）

```
mysql> create table a(
    -> a_id int primary key auto_increment,
    -> a_name varchar(20) not null
    -> );
Query OK, 0 rows affected (0.01 sec)

mysql> desc a;
+--------+-------------+------+-----+---------+----------------+
| Field  | Type        | Null | Key | Default | Extra          |
+--------+-------------+------+-----+---------+----------------+
| a_id   | int(11)     | NO   | PRI | NULL    | auto_increment |
| a_name | varchar(20) | NO   |     | NULL    |                |
+--------+-------------+------+-----+---------+----------------+
2 rows in set (0.00 sec)
```

表B （B表中的fy_id字段，只能添加a\_id中 已有的数据_

```
mysql> create table b(
    -> b_id int primary key,
    -> b_name varchar(20) not null,
    -> fy_id int not null,
    -> foreign key(fy_id) references a(a_id)
    -> );
Query OK, 0 rows affected (0.08 sec)

mysql> desc b;
+--------+-------------+------+-----+---------+-------+
| Field  | Type        | Null | Key | Default | Extra |
+--------+-------------+------+-----+---------+-------+
| b_id   | int(11)     | NO   | PRI | NULL    |       |
| b_name | varchar(20) | NO   |     | NULL    |       |
| fy_id  | int(11)     | NO   | MUL | NULL    |       |
+--------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)
```

##### 删除外键

删除外键指定别名方法：

    mysql> show create table b;
    +-------+-----------------------------------------------------------------+
    | Table | Create Table                                                     
    +-------+-----------------------------------------------------------------+
    | b     | CREATE TABLE `b` (
      `b_id` int(11) NOT NULL,
      `b_name` varchar(20) NOT NULL,
      `fy_id` int(11) NOT NULL,
      PRIMARY KEY (`b_id`),
      KEY `AB_id` (`fy_id`),
      CONSTRAINT `AB_id` FOREIGN KEY (`fy_id`) REFERENCES `a` (`a_id`)
    ) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci |
    +-------+----------------------------------------------------------------+
    1 row in set (0.00 sec)

    mysql> alter table b drop foreign key AB_id;
    Query OK, 0 rows affected (0.11 sec)
    Records: 0  Duplicates: 0  Warnings: 0

删除随机外键别名方法：

    mysql> show create table b;
    +-------+----------------------------------------------------------------+
    | Table | Create Table                                                   |
    +-------+----------------------------------------------------------------+
    | b     | CREATE TABLE `b` (
      `b_id` int(11) NOT NULL,
      `b_name` varchar(20) NOT NULL,
      `fy_id` int(11) NOT NULL,
      PRIMARY KEY (`b_id`),
      KEY `fy_id` (`fy_id`),
      CONSTRAINT `b_ibfk_1` FOREIGN KEY (`fy_id`) REFERENCES `a` (`a_id`)
    ) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci |
    +-------+----------------------------------------------------------------+
    1 row in set (0.00 sec)

    mysql> alter table b drop foreign key b_ibfk_1;
    Query OK, 0 rows affected (0.08 sec)
    Records: 0  Duplicates: 0  Warnings: 0

##### 增加外键

指定外键别名方法一：

    mysql> alter table b
        -> add constraint AB_id foreign key (fy_id) references a(a_id);
    Query OK, 0 rows affected (0.04 sec)
    Records: 0  Duplicates: 0  Warnings: 0

    mysql> show create table b;
    +-------+----------------------------------------------------------------+
    | Table | Create Table                                                   |
    +-------+----------------------------------------------------------------+
    | b     | CREATE TABLE `b` (
      `b_id` int(11) NOT NULL,
      `b_name` varchar(20) NOT NULL,
      `fy_id` int(11) NOT NULL,
      PRIMARY KEY (`b_id`),
      KEY `AB_id` (`fy_id`),
      CONSTRAINT `AB_id` FOREIGN KEY (`fy_id`) REFERENCES `a` (`a_id`)
    ) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci |
    +-------+----------------------------------------------------------------+
    1 row in set (0.00 sec)

随机外键别名方法二：

    mysql> alter table b
        -> add foreign key (fy_id) references a(a_id);
    Query OK, 0 rows affected (0.06 sec)
    Records: 0  Duplicates: 0  Warnings: 0

    mysql> show create table b;
    +-------+----------------------------------------------------------------+
    | Table | Create Table                                                   |
    +-------+----------------------------------------------------------------+
    | b     | CREATE TABLE `b` (
      `b_id` int(11) NOT NULL,
      `b_name` varchar(20) NOT NULL,
      `fy_id` int(11) NOT NULL,
      PRIMARY KEY (`b_id`),
      KEY `fy_id` (`fy_id`),
      CONSTRAINT `b_ibfk_1` FOREIGN KEY (`fy_id`) REFERENCES `a` (`a_id`)
    ) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci |
    +-------+----------------------------------------------------------------+
    1 row in set (0.00 sec)

##### 查看表使用那些命令

    mysql> show create table b;
    +-------+----------------------------------------------------------------+
    | Table | Create Table                                                   |
    +-------+----------------------------------------------------------------+
    | b     | CREATE TABLE `b` (
      `b_id` int(11) NOT NULL,
      `b_name` varchar(20) NOT NULL,
      `fy_id` int(11) NOT NULL,
      PRIMARY KEY (`b_id`),
      KEY `AB_id` (`fy_id`),
      CONSTRAINT `AB_id` FOREIGN KEY (`fy_id`) REFERENCES `a` (`a_id`)
    ) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci |
    +-------+----------------------------------------------------------------+
    1 row in set (0.00 sec)



