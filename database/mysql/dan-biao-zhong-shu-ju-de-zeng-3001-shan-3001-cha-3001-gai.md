#### MySQL  insert插入数据

#### insert 语法一

##### insert \[into\] table\__name \[\(column\_name_\)\] {values\|value}

##### 插入单条数据

```
mysql> insert into test (id,name) value(1,'Rave');
Query OK, 1 row affected (0.03 sec)
```

##### 插入多条数据

```
mysql> insert into test(id,name) value(2,'leva'),(3,'zlk');
Query OK, 2 rows affected (0.02 sec)
Records: 2  Duplicates: 0  Warnings: 0
```

#### insert 语法二

##### insert \[into\] table_name set col\_name = {expr\|default}_

```
mysql> insert into test set id = 4,name = 'akai';
Query OK, 1 row affected (0.04 sec)
```

#### select 查询 语法

##### 查询表内所有数据   \* 表示所有内容

##### select \* from table\_name \[where\];

```
mysql> select * from test;
+------+------+
| id   | name |
+------+------+
|    1 | Rave |
|    2 | leva |
|    3 | zlk  |
|    4 | akai |
+------+------+
4 rows in set (0.00 sec)
```

##### 只查询表内指定字段内容

```
mysql> select name from test;
+------+
| name |
+------+
| Rave |
| leva |
| zlk  |
| akai |
+------+
4 rows in set (0.00 sec)
```

##### 只查询表内指定字段与条件内容

```
mysql> select name from test where id >2;
+------+
| name |
+------+
| zlk  |
| akai |
+------+
2 rows in set (0.00 sec)
```

#### update更新数据

##### select 查询 语法

##### update table_name set col\_name1={expr1\|default} \[where\]_

##### 例子：将id = 3 的name 修改为‘不动’

```
mysql> update test set name = '不动' where id = 3;
Query OK, 1 row affected (0.06 sec)
Rows matched: 1  Changed: 1  Warnings: 0
```

#### delete 删除   语法

##### delete from table\_name where where\_conditon;

注意：一定要写where条件，不然会删除全部数据。

##### 例子：将id = 1 的数据删除

```
mysql> delete from test where id = 1;
Query OK, 1 row affected (0.04 sec)
```

#### 表结构 增、删、改、查

##### 表结构 增  add

在表结构内第一行增加一个字段

```
mysql> create table tb1(
    -> id int,
    -> name char(4)
    -> );
Query OK, 0 rows affected (0.08 sec)

mysql> alter table tb1
    -> add age int first;    ##插入列内第一行数据
Query OK, 0 rows affected (0.07 sec)
Records: 0  Duplicates: 0  Warnings: 0
```

在表结构内插入到指定位置指定字段

```
mysql> alter table tb1
    -> add age int after id;     ##after表示插入到指定字段后面
Query OK, 0 rows affected (0.02 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc tb1;
+-------+---------+------+-----+---------+-------+
| Field | Type    | Null | Key | Default | Extra |
+-------+---------+------+-----+---------+-------+
| id    | int(11) | YES  |     | NULL    |       |
| age   | int(11) | YES  |     | NULL    |       |
| name  | char(4) | YES  |     | NULL    |       |
+-------+---------+------+-----+---------+-------+
3 rows in set (0.00 sec)
```

##### 表结构 删 drop

```
+-------+---------+------+-----+---------+-------+
| Field | Type    | Null | Key | Default | Extra |
+-------+---------+------+-----+---------+-------+
| id    | int(11) | YES  |     | NULL    |       |
| age   | int(11) | YES  |     | NULL    |       |
| name  | char(4) | YES  |     | NULL    |       |
+-------+---------+------+-----+---------+-------+
3 rows in set (0.00 sec)

mysql> alter table tb1
    -> drop age;
Query OK, 0 rows affected (0.07 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc tb1;
+-------+---------+------+-----+---------+-------+
| Field | Type    | Null | Key | Default | Extra |
+-------+---------+------+-----+---------+-------+
| id    | int(11) | YES  |     | NULL    |       |
| name  | char(4) | YES  |     | NULL    |       |
+-------+---------+------+-----+---------+-------+
2 rows in set (0.01 sec)
```

##### 表结构 改 （数据类型方法 modify 字段名称方法 change 改表名rename）

修改表结构内数据类型方法

```
mysql> alter table tb1
    -> modify name varchar(10);  ## 改表结构数据类型
Query OK, 0 rows affected (0.03 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc tb1;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int(11)     | YES  |     | NULL    |       |
| name  | varchar(10) | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
2 rows in set (0.00 sec)
```

改表结构字段名称

```
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int(11)     | YES  |     | NULL    |       |
| name  | varchar(10) | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
2 rows in set (0.00 sec)

mysql> alter table tb1
    -> change name sex char(4);  ##修改字段名称以及属性类型
Query OK, 0 rows affected (0.06 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc tb1;
+-------+---------+------+-----+---------+-------+
| Field | Type    | Null | Key | Default | Extra |
+-------+---------+------+-----+---------+-------+
| id    | int(11) | YES  |     | NULL    |       |
| sex   | char(4) | YES  |     | NULL    |       |
+-------+---------+------+-----+---------+-------+
2 rows in set (0.00 sec)
```

改表名方法

```
+----------------+
| Tables_in_mydb |
+----------------+
| tb2            |
+----------------+
6 rows in set (0.00 sec)

mysql> alter table tb2
    -> rename tb1;    ## 表改名
Query OK, 0 rows affected (0.06 sec)

mysql> show tables;
+----------------+
| Tables_in_mydb |
+----------------+
| tb1            |
+----------------+
6 rows in set (0.00 sec)
```

##### 表结构 查

show create table tablename

    mysql> desc tb1; ##看看表结构方法
    +-------+---------+------+-----+---------+-------+
    | Field | Type    | Null | Key | Default | Extra |
    +-------+---------+------+-----+---------+-------+
    | id    | int(11) | YES  |     | NULL    |       |
    | sex   | char(4) | YES  |     | NULL    |       |
    +-------+---------+------+-----+---------+-------+
    2 rows in set (0.00 sec)

    mysql> show create table tb1\G  ##查看表使用了那些命令
    *************************** 1. row ***************************
           Table: tb1
    Create Table: CREATE TABLE `tb1` (
      `id` int(11) DEFAULT NULL,
      `sex` char(4) DEFAULT NULL
    ) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci
    1 row in set (0.00 sec)



