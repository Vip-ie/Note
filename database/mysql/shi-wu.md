#### 事务（Transaction）详解

##### 一、事务定义

* Transaction
* 事务：一个最小的不可再分的工作单元；通常一个事务对应一个完整的业务（例如银行账户转账业务，该业务就是一个最小的工作单元）
* 一个完整的业务需要批量的DML（insert、update、delete）语句共同联合完成
* 事务只和DML语句有关，或者说DML语句才有事务。这个和业务罗技有关，业务逻辑不同，DML语句的数不同

---

##### 二、转账操作理解事务

关于银行账户转账操作，账户转账是一个完整的业务，最小的单元，不可再分，也就是说银行账户转账是一个事务

以下是银行账户表t\_act（账号、余额），进行转账操作

```
actno       balance
1           500
2           100
转账操作
update t_act set balance=400 where actno=1;
update t_act set balance=200 where actno=2;
```

以上两台DML语句必须同时成功或者同时失败。最小单元不可再分，当第一条DML语句执行成功后，并不能将底层数据库中的第一个账户的数据修改，只是将操作记录了一下；这个记录是在内存中完成的；当第二条DML语句执行成功后，和底层数据库文件中的数据完成同步。若第二条DML语句执行失败，则清空所有的历史操作记录，要完成以上的功能必须借助事务

---

##### 三、事务四大特征（ACID\)

* 原子性\(A\):事务是最小单位，不可再分
* 一致性\(C\):事务要求所有的DML语句操作的时候，必须保证同时成功或者同时失败
* 隔离性\(I\):事务A和事务B之间具有隔离性
* 持久性\(D\):是事务的保证，事务终结的标志（内存的数据持久到硬盘文件中）

---

##### 四、关于事务的一些术语

* 开启事务:start transaction
* 事务结束:end transaction
* 提交事务: commit transaction
* 回滚事务:rollback transaction

---

##### 五、和事务相关的两个重要的SQL语句\(TCL\)

* commit:提交
* rollback:回滚

---

##### 六、事务开启与结束标志

开启标志:

* 任何一条DML语句（insert、update、delete）执行，标志事务的开启

结束标志（提交或者回滚）

* 提交:成功的结束，将所有的DML语句操作历史记录和底层硬盘数据来一次同步
* 回滚:失败的结束，将所有的DML语句操作历史记录全部清空

---

##### 七、事务与数据库底层数据

在事务进行过程中，未结束之前，DML语句是不会更改底层数据，只有将历史操作记录一下，在内存中完成记录。只有在事务结束的时候，而且是成功的结束的时候，才会改写底层硬盘文件中的数据。

---

##### 八、在MySQL中，事务提交与回滚

在mysql中，默认情况下，事务是自动提交的，也就是说，只要执行一条DML语句就开启了事务，并且提交了事务。

以上的自动提交机制是可以关闭的，对t\_user进行提交和回滚操作

**提交操作\(事务成功\)**

* start transaction
* DML语句
* commit

```
mysql> start transaction;手动开启事务
mysql> insert int t_user(name) value('pp');
mysql> commit;commit之后即可改变底层数据库数据
mysql> select * from from t_user;
+----+------+
| id | name |
+----+------+
|  1 | jay  |
|  2 | man  |
|  3 | pp   |
+----+------+
3 rows in set (0.00 sec)
```

##### 回滚操作\(事务失败\)

* start transaction
* DML语句
* rollback

```
mysql> start transaction;
mysql> insert into t_user(name) values('yy');
mysql> rollback;
mysql> select * from t_user;
+----+------+
| id | name |
+----+------+
|  1 | jay  |
|  2 | man  |
|  3 | pp   |
+----+------+
3 rows in set (0.00 sec)
---------------------
```

---

##### 九、事务四大特性之一 隔离性（isolation）

1. 事务A和事务B之间具有一定的隔离性
2. 隔离性有隔离级别\(4\)

> 1. 读未提交:read uncommitted
> 2. 读已提交:read committed
> 3. 可重复读:repeatableread
> 4. 串行化:serializable

1、read uncommitted

```
- 事物A和事物B，事物A未提交的数据，事物B可以读取到
- 这里读取到的数据叫做“脏数据”
- 这种隔离级别最低，这种级别一般是在理论上存在，数据库隔离级别一般都高于该级别
```

2、read committed

```
- 事物A和事物B，事物A提交的数据，事物B才能读取到
- 这种隔离级别高于读未提交
- 换句话说，对方事物提交之后的数据，我当前事物才能读取到
- 这种级别可以避免“脏数据”
- 这种隔离级别会导致“不可重复读取”
- Oracle默认隔离级别
```

3、repeatable read

```
- 事务A和事务B，事务A提交之后的数据，事务B读取不到
- 事务B是可重复读取数据
- 这种隔离级别高于读已提交
- 换句话说，对方提交之后的数据，我还是读取不到
- 这种隔离级别可以避免“不可重复读取”，达到可重复读取
- 比如1点和2点读到数据是同一个
- MySQL默认级别
- 虽然可以达到可重复读取，但是会导致“幻像读”
```

4、serializable

```
- 事务A和事务B，事务A在操作数据库时，事务B只能排队等待
- 这种隔离级别很少使用，吞吐量太低，用户体验差
- 这种级别可以避免“幻像读”，每一次读取的都是数据库中真实存在数据，事务A与事务B串行，而不并发
```

---

##### 十、隔离级别与一致性关系

| 隔离级别 | 脏读取 | 不可重复读 | 幻像读 |
| :--- | :--- | :--- | :--- |
| 读未提交 | 可能 | 可能 | 可能 |
| 度已提交 | 不可能 | 可能 | 可能 |
| 可重复读 | 不可能 | 不可能 | 对InnoBD不可能 |
| 串行化 | 不可能 | 不可能 | 不可能 |

##### 十一、设置事务隔离级别

方式一

可以在my.ini文件中使用transaction-isolation选项来设置服务器的缺省事务隔离界别

* 该选项可以是

```
– READ-UNCOMMITTED
– READ-COMMITTED
– REPEATABLE-READ
– SERIALIZABLE

•   例如：
[mysqld]
transaction-isolation = READ-COMMITTED
```

方式二

通过命令动态设置隔离界别

* 隔离级别也可以运行在服务器中动态设置，应使用set transaction isolation level语句
* 其语法模式为

```
SET [GLOBAL | SESSION] TRANSACTION ISOLATION LEVEL <isolation-level>
其中的<isolation-level>可以是：
– READ UNCOMMITTED
– READ COMMITTED
– REPEATABLE READ
– SERIALIZABLE
• 例如： SET TRANSACTION ISOLATION LEVEL REPEATABLE READ;
```

##### 十二、隔离级别的作用范围

```
•   事务隔离级别的作用范围分为两种： 
–   全局级：对所有的会话有效 
–   会话级：只对当前的会话有效 
•   例如，设置会话级隔离级别为READ COMMITTED ：
mysql> SET TRANSACTION ISOLATION LEVEL READ COMMITTED；
或：
mysql> SET SESSION TRANSACTION ISOLATION LEVEL READ COMMITTED；
•   设置全局级隔离级别为READ COMMITTED ： 
mysql> SET GLOBAL TRANSACTION ISOLATION LEVEL READ COMMITTED；
```

---

##### 十三、查看隔离界别

```
•   事务隔离级别的作用范围分为两种： 
–   全局级：对所有的会话有效 
–   会话级：只对当前的会话有效 
•   例如，设置会话级隔离级别为READ COMMITTED ：
mysql> SET TRANSACTION ISOLATION LEVEL READ COMMITTED；
或：
mysql> SET SESSION TRANSACTION ISOLATION LEVEL READ COMMITTED；
•   设置全局级隔离级别为READ COMMITTED ： 
mysql> SET GLOBAL TRANSACTION ISOLATION LEVEL READ COMMITTED；
```



