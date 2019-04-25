#### python操作mysql

要操作数据库，首先就要建立和数据库的连接，配置pymysql.connect连接数据库：

```
import pymysql              #导入pymysql模块

conn = pymysql.connect(
    host = '127.0.0.1',     #主机IP
    port = 3306,            #端口
    user = 'leva',          #用户名
    password = 'leva123',   #密码
    db = 'mydb',            #数据库名
    charset = 'utf8'        #数据库编码
)
print(conn)                 #测试连接数据库是否成功
```

##### 定义游标

```
#定义游标
cursor = conn.cursor()
```

##### 执行SQL语句

```
cursor.execute('show tables')
```

##### 取出数据

```
cursor.fetchone()   #取出一条数据
cursor.fetchall()   #取出所有数据

取出数据例：
date_tb ='''
select * from student
'''
cursor.execute(date_tb)
one = cursor.fetchone()
print(*one)
结果
1 zlk 1
```

##### 创建表

```
tb = '''
create table tb(
id int primary key auto_increment,
name varchar(20)
)
'''
cursor.execute(tb)
```

##### 插入

```
row = cursor.execute("insert into tb(id,name)value(1,'zlk')")
conn.commit()   #提交事务
cursor.close()  #关闭游标
conn.close()    #关闭连接
```

##### 更新

```
row = cursor.execute("update test set name= '三花' where id = %s", (2,))
conn.commit()   #提交事务
cursor.close()  #关闭游标
conn.close()    #关闭连接
```

##### 删除

```
row = cursor.execute("delete from tb where id = 3")
conn.commit()   #提交事务
cursor.close()  #关闭游标
conn.close()    #关闭连接
```

##### 联合查询

```
union ='''
select s_name as 姓名,tz_name as 学院,c_name as 课程 from student 
left join tanzhou on ts_id=tz_id
left join course on tz_id=tzc_id
left join choose on cc_id=c_id
'''
cursor.execute(union)
one = cursor.fetchone()   #取出一条数据
all = cursor.fetchall()   #取出所有数据
print（*all）             
('zlk', '软件', 'java') 
('lezlk', '语言', 'english') 
('rave', '营销', 'seo') 
('rac', '其他', '其他') 
('hzip', '设计', None)
```



