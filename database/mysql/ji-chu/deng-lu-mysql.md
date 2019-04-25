#### 登录MySQL

```
mysql -u + user -p + password；
```

#### 创建用户

```
mysql>create user 'leva'@'%' identified by 'leva123';
```

#### 给用户赋予权限

```
mysql>grant all on *.* to 'leva'@'%';
```

#### 使更改立即生效

```
mysql>flush privileges;
```

#### 退出

```
mysql>\q
mysql>exit
```

#### 查看当前用户

```
select user();
```

#### 查看当前数据库

```
select database（）;
```

#### 设置数据库编码为utf8

    mysql> alter database zy character set utf8;
    Query OK, 1 row affected, 1 warning (0.03 sec)

    查看数据库编码
    mysql> show create database zy\G
    *************************** 1. row ***************************
           Database: zy
    Create Database: CREATE DATABASE `zy` /*!40100 DEFAULT CHARACTER SET utf8 */
    1 row in set (0.00 sec)



