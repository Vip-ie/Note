#### MySQL数据类型

##### 常用的4种：整型、浮点型、日期类型、字符

```
mysql> create table st(
    -> id int,                    ## 整型
    -> name varchar(20),          ## 指定长度，最多65535个字符
    -> sex char(4),               ## 指定长度，最多255个字符，定长
    -> price double(4,2),         ## 双精度浮点型，m总个数，d小数为
    -> detail text,               ## 可变长度，最多65535个字符
    -> dates datetime,            ## 日期时间类型 YYYY-MM-DD HH:MM:SS
    -> ping enum('好评','差评')    ## 枚举，在给出的value中选择
    -> );
```

```
insert into table vale(1,‘裤子’，‘男’，20.0，‘这条裤子超好！！！’，now(),'好评')；
```



