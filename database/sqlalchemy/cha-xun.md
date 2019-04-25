## SQLAlchemy 查询

1. **过滤函数必须掌握：两个过滤函数的用法和区别**
2. **函数必须掌握：使用函数的方法**
3. **排序必须掌握：排序方法和分组等方法**
4. **模糊查询必须掌握：常见的模糊查询方法**

## **创建一个数据库连接文件connect.py**

```py
from sqlalchemy.ext.declarative import declarative_base  #引入Base类才可以创建基类
from sqlalchemy.orm import sessionmaker #创建会话

# 大写字母定义变量一般作为常量使用
HOSTNAME= '127.0.0.1'
PORT= '3306'
DATABASE = 'orm'
USERNAME = 'leva'
PASSWORD = 'leva123'

Db_url = 'mysql+pymysql://{}:{}@{}:{}/{}?charset=utf8'.format(
    USERNAME,
    PASSWORD,
    HOSTNAME,
    PORT,
    DATABASE
)

engine = create_engine(Db_url)   #实例化一个对象

Base = declarative_base(engine)  #创建一个Base基类
Session = sessionmaker(engine) #创建一个实例会话
session = Session() #实例一个对象
```

## **创建一个数据库模型文件user\_modules.py**

```py
from datetime import datetime
from sqlalchemy import Column, Integer, String, DateTime, Boolean

class User(Base):
    """建立数据库模型对应User表"""
    __tablename__ ='user'
    id = Column(Integer, primary_key=True, autoincrement= True)
    username = Column(String(20))
    password = Column(String(20))
    create_time = Column(DateTime, default=datetime.now())
    _locked = Column(Boolean, default=False, nullable=False)

    def __repr__(self):
        return "<User(id=%s),username=%s,password=%s,create_time=%s, _locked=%s>"%(
            self.id,
            self.username,
            self.password,
            self.create_time,
            self._locked
        )
```

## **创建一个查询文件query\_test.py**

```py
from connect import session
from user_modules import User

query返回对象
rs = session.query(User).filter(User.username=='vip')
print(rs,type(rs))
#query根据返回结果来看，rs是一个Query对象，打印出来可以看到转化的 SQL
使用SQLAlchemy时，如果想要查看最终在数据库中执行的sql，可以通过上述方式来查看

返回列表对象
rs = session.query(User).filter(User.username=='vip')
print(rs,type(rs))

all返回列表
rs = session.query(User).filter(User.username=='vip').all()
print(rs,type(rs))
#在query中查询对象的某个属性值 ( 对应为查询表中某个字段的值 )，返回的结果不再是一个 Query 对象，而是一个列表

first 是返回所有符合条件数据的第一条数据
rs = session.query(User).filter(User.username=='vip').first()
#first 返回一个元组对象

[0]
rs = session.query(User).filter(User.username=='vip')[0]
print(rs,type(rs))
返回一个类对象
#[0] 和 first 类似，但是如果没有符合条件的数据则会报错

取值方式
rs = session.query(User).filter(User.username=='vip').all()
print(rs,type(rs))
#这两种方式可以取到具体的数据值
```

## **filter过滤函数**

```py
from connect import session
from user_modules import User

rs = session.query(User).filter(User.username=='vip').all()
#filter 是一个过滤函数，过滤条件都可以书写在此函数中，不同的条件之间用 逗号 分隔

filter_by
rs = session.query(User).filter_by(User.username=='vip').all()
#filter_by 也是一个过滤函数，但是功能要弱一些

filter 和 filter_by 的区别
二者都是 过滤函数，但是使用有如下差别：
1. filter 中需要添加 类对象，filter_by不需要
2. filter_by 中只能添加等于的条件，不能添加 不等于、大于小于等条件，filter没有这个限制
```

## **模糊查询**

**like和notlike**

* like是模糊查询，和数据库中的like用法一样
* notlike和like作用相反

```py
rs = session.query(User.id).filter(User.username.like('vip')).all()
print(rs,type(rs))
#返回一个列表
rs = session.query(User.id).filter(User.username.like('v%')).all()
print(rs,type(rs))
```

**in\_  和 notin\_**

in\_和notin\_是范围查找

```py
rs = session.query(User.id).filter(User.username.in_(['vip','tuple'])).all()
print(rs,type(rs))

rs = session.query(User.id).filter(User.username.notin_(['vip','tuple'])).all()
print(rs,type(rs))
```

**is\_和isnot**

is\_和isnot 精确查找

```py
rs = session.query(User.id).filter(User.username.is_(None)).all()
print(rs,type(rs))

rs = session.query(User.id).filter(User.username.isnot(None)).all()
print(rs,type(rs))
```

**查看结果数**

```py
all 查看所有数据
rs = session.query(User.username).filter(User.username!='vip').all()
print(rs,type(rs))

limit 查看指定条数数据
rs = session.query(User.username).filter(User.username!='vip')limit(2).all()
print(rs,type(rs))

offset 偏移一条记录
rs = session.query(User.username).filter(User.username!='vip').offset(1).all()
print(rs,type(rs))

slice 对查询出来的数据进行切片取值
rs = session.query(User.username).filter(User.username!='vip').slice(1,3).all()
print(rs,type(rs))

one 查询一条数据，如果不存在多条则报错
rs = session.query(User.username).filter(User.username=='tuple').one()
print(rs,type(rs))
```

**排序**

```py
from connect import session
from user_modules import User
from sqlalchemy import desc  #导入模块

order_by
session.query(User.username).filter(User.username!='vip').order_by(User.id).all()

#导入desc模块
desc
rs = session.query(User.username).filter(User.username!='vip').order_by(desc(User.id)).all()
print(rs,type(rs))

order_by  和 limit 一起使用的时候，可以通过如上方式
rs = session.query(User.id).filter(User.username!='vip').order_by(desc(User.id)).limit(2).all()
print(rs,type(rs))
```

**函数**

```py
from connect import session
from user_modules import User
from sqlalchemy import desc 
from sqlalchemy import func.extract #函数模块

func.count(统计函数)
我们统计出密码相同为分组统计出来所有信息
rs = session.query(User.password,func.count(User.id)).group_by(User.password).all()

having 也可以直接使用，使用方法也和 SQL 中使用类似
rs = session.query(User.password, func.count(User.id)).group_by(User.password).having(func.count(User.id)>1).all()

这里只是给出一个演示实例，如果在今后需要使用其他的函数，导入即可
extract函数
extract 提取对象中的数据，这里提取分钟，并把提取出来的结果用 label 命名别名，之后就可以使用 group_by 来分组
rs = session.query(extract('minute',User.create_time).label('minute'),func.count(User.id)).group_by('minute').all()

extract函数
count 里面同样可以使用 * 
rs = session.query(extract('day',User.create_time).label('day'), func.count('*')).group_by('day').all()
```

**聚合函数分组**

```py
from connect import session
from user_modules import User
from sqlalchemy import func #函数模块

func.sum求和
rs = session.query(User.password, func.sum(User.id)).group_by(User.password).all()

func.max求最大值
rs = session.query(User.password, func.max(User.id)).group_by(User.password).all()

func.min求最小值
rs = session.query(User.password, func.min(User.id)).group_by(User.password).all()
```

**选择条件**

```py
from connect import session
from user_modules import User
from sqlalchemy import or_

or_  是或者的意思，和数据库中的 or 一样
rs = session.query(User.username).filter(or_(User.username.isnot(None),User.password=='123')).all()
```



