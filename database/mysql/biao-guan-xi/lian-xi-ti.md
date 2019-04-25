#### 练习题

##### 1.建立选课系统中的5张表：（学院表，学生表，学生详情表，课程表，选课表），并每张表插入4条数据。

创建学院college 字段有 id 分类

```
mysql> create table college(
    -> id int primary key,
    -> f_name varchar(20)
    -> );
Query OK, 0 rows affected (0.06 sec)
```

创建课程表course创建字段有id 课程分类

```
mysql> create table course(
    -> id int primary key,
    -> c_name varchar(20)
    -> );
Query OK, 0 rows affected (0.11 sec)
```

创建学生表student创建字段有id、课程名字

```
mysql> create table student(
    -> id int primary key auto_increment,
    -> s_name varchar(20)
    -> );
Query OK, 0 rows affected (0.06 sec)
```

创建逻辑表logic创建字段有id、课程id 联合主键 关系

```
mysql> create table logice(
    -> l_id int not null,
    -> c_id int not null,
    -> primary key (l_id,c_id),
    -> foreign key (l_id) references student(id),
    -> foreign key (c_id) references course(id)
    -> );
Query OK, 0 rows affected (0.12 sec)
```

创建学生详情表details 创建字段id、出生年月、性别、地址、电话、email

```
mysql> create table details(
    -> id int not null,
    -> age int not null,
    -> sex char(4),
    -> adder varchar(20),
    -> tel int not null,
    -> email varchar(20)
    -> );
Query OK, 0 rows affected (0.10 sec)
```

##### 2.用文字描述：这5张表之间，对应的关系，并说明如何实现这个对应关系。



