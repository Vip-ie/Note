#### 创建数据库   语法

##### create database \[in not exists\]    重复创建会报错，所以可以加上if not exists

**注意：**SQL语句必须以分号结尾。

```
mysql> create database mydb;
Query OK, 1 row affected (0.06 sec)
```

#### 查看有那些数据库

```
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mydb               |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
6 rows in set (0.00 sec)
```

#### 删除数据库     语法

##### drop database \[in exists\]  dbname;

##### 如果不知道数据库，是否存在记得加if exists。

```
mysql> drop database mydb;
Query OK, 0 rows affected (0.11 sec)

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
5 rows in set (0.01 sec)
```

#### Mysql数据库使用

##### 查看在哪个数据库里

##### select database\(\);

```
mysql> select database();
+------------+
| database() |
+------------+
| NULL       |    NULL表示没有进入任何数据库，其他名字表示数据名
+------------+
1 row in set (0.00 sec)
```

#### 进入 数据库 语法

##### use dbname;          注意：数据库创建成功，并没有直接使用

```
mysql> use college
Database changed

mysql> select database();
+------------+
| database() |
+------------+
| college    |
+------------+
1 row in set (0.00 sec)
```



