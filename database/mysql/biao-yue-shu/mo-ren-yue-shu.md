#### 默认约束 default

##### default： 初始值设置，插入记录时，如果没有明确为字段复制，则自动赋值默认值。

##### 例子

```
mysql> create table tb6(
    ->    id int primary key auto_increment,
    ->    name varchar(20) not null,
    ->    age int not null default 18
    -> );
Query OK, 0 rows affected (0.04 sec)

mysql> desc tb6;
+-------+-------------+------+-----+---------+----------------+
| Field | Type        | Null | Key | Default | Extra          |
+-------+-------------+------+-----+---------+----------------+
| id    | int(11)     | NO   | PRI | NULL    | auto_increment |
| name  | varchar(20) | NO   |     | NULL    |                |
| age   | int(11)     | NO   |     | 18      |                |
+-------+-------------+------+-----+---------+----------------+
3 rows in set (0.00 sec)
```

##### 删除default

```
mysql> alter table tb6
    -> modify age int;
Query OK, 0 rows affected (0.10 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc tb6;
+-------+-------------+------+-----+---------+----------------+
| Field | Type        | Null | Key | Default | Extra          |
+-------+-------------+------+-----+---------+----------------+
| id    | int(11)     | NO   | PRI | NULL    | auto_increment |
| name  | varchar(20) | NO   |     | NULL    |                |
| age   | int(11)     | YES  |     | NULL    |                |
+-------+-------------+------+-----+---------+----------------+
3 rows in set (0.00 sec)
```

##### 添加默认值default

```
mysql> alter table tb6
    -> modify age int default 20;
Query OK, 0 rows affected (0.10 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc tb6;
+-------+-------------+------+-----+---------+----------------+
| Field | Type        | Null | Key | Default | Extra          |
+-------+-------------+------+-----+---------+----------------+
| id    | int(11)     | NO   | PRI | NULL    | auto_increment |
| name  | varchar(20) | NO   |     | NULL    |                |
| age   | int(11)     | YES  |     | 20      |                |
+-------+-------------+------+-----+---------+----------------+
3 rows in set (0.00 sec)
```



