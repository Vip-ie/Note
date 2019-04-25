## SQLAlchemy 多表查询

1. **必须掌握：多表查询时join方法**
2. **必须掌握：子表的使用方法**

**创建一个connect.py文件**

```py
from sqlalchemy import create_engine
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

**创建一个user\_modules.py文件**

```py
from connect import Base
from datetime import datetime
from sqlalchemy import Column, Integer, String, DateTime, Boolean, ForeignKey, Table #ForeignKey导入一个外键包
from sqlalchemy.orm import relationship #导入relationship包

-------------------------------------------------------------------------------------
#一对多表查询
#一对一表查询
#多对多表查询
class User(Base):
    """建立数据库模型对应User表"""
    __tablename__ ='user'
    id = Column(Integer, primary_key=True, autoincrement= True)
    username = Column(String(20))
    password = Column(String(20))
    create_time = Column(DateTime, default=datetime.now())
    _locked = Column(Boolean, default=False, nullable=False)

    def __repr__(self):
        return "<User(id=%s,username=%s,password=%s,create_time=%s, _locked=%s)>"%(
            self.id,
            self.username,
            self.password,
            self.create_time,
            self._locked
        )

-------------------------------------------------------------------------------------
#一对多表查询
#一对一表查询
class UserDetails(Base):
    __tablename__= 'user_details'
    id = Column(Integer, primary_key=True, autoincrement=True)  #primary_key是否为主键True是 False否 autoincrement是否为自增长，True是，False否
    id_card = Column(Integer, nullable=True, unique=True)   #nullable是否为空，True是，False 否
    lost_login = Column(DateTime)
    login_num = Column(Integer, default=0)
    user_id = Column(Integer,ForeignKey('user.id'))

# sqlalchemy.orm导入relationship包     
    userdetail = relationship('User', backref = 'details', uselist = True, cascade = 'all')#申明一下表关系
#backref声明一个属性，在前面设置有关表类的名称，表示为这个表增加属性
#uselist = False True表示一对多关系，False表示一对一关系
#cascade = ‘all' 所有的可选字符串项

    def __repr__(self):
        return'<UserDetails(id=%s, id_card=%s, last_login=%s, login_num=%s, user_id=%s)>'%(
            self.id,
            self.id_card,
            self.lost_login,
            self.login_num,
            self.user_id
        )
-------------------------------------------------------------------------------------
#多对多表查询
class Article(Base):
    __tablename__ ='article'
    id = Column(Integer, primary_key=True, autoincrement=True)
    content = Column(String(500), nullable=True)
    create_time = Column(DateTime, default=datetime.now)

# sqlalchemy.orm导入relationship包   
#article_user = relationship('User', backref='article', secondary='user_article')#申明表关系
#backref 增加一个属性到中间表user_article, secondary中间表属性

    def __repr__(self):
        return "Article(id=%s, content=%s, create_time=%s)"%(
        self.id,
        self.content,
        self.create_time
    )

-------------------------------------------------------------------------------------
#导入sqlalchemy中的Table包
#多对多中间表
user_article = Table('user_article', Base.metadata,
                    Column('user_id', Integer, ForeignKey('user.id'), primary_key=True),
                    Column('article_id', Integer, ForeignKey('article.id'),primary_key=True)
                    )
```

**创建一个query\_test.py文件**

```py
from connect import session
from user_modules import User, UserDetails

cross join这种是 通过打印的 SQL 来看， 
rs = session.query(User,UserDetails)

示例：
rs = session.query(User,UserDetails).filter(User.username==UserDetail.id_card).all()
print(rs,type(rs))

通过打印的 SQL 来看 下面这种方式是 inner join
rs = session.query(User.username,UserDetails.id_card).join(UserDetails,UserDetails.user_id==User.id).all()


通过上面打印的  SQL 来看， 下面这种方式采用的是left join
rs = session.query(User.username,UserDetails.id_card).outerjoin(UserDetails,UserDetails.user_id==User.id).all()

union 是联合查询，有自动去重的功能，对应的还有 union_all
q1 = session.query(User.id)
q2 = session.query(UserDetails.id)
print(q1.union(q2).all())

subquery声明子表
sql_0 = session.query(UserDetails.lost_login).subquery()

subquery声明子表使用
rs = session.query(User,sql_0.c.lost_login).all()
```

**原生SQL查询**

必须掌握：原生SQL的使用方法

```py
sql_1 ="""
    select * from `user`
"""
查询
row = session.execute(sql_1)
取值
print(row.fetchone())
print(row.fetchmany())
print(row.fetchall())

循环取值
for i in row:
    print(i)
```

**一对一或一对多查询查询**

创建一个quey\_test.py文件

```py
from connet import session
from user_modules import User, UserDetails

if __name__ == "__main__":
    rows = session.query(User).get(3) #查询User表中id为3的数据
    print(rows.details)
```

**多对多表查询**

```py
from connect import session
from user_modules import User, UserDetails, Article


if __name__ == "__main__":

    ros = session.query(Article).get(2)
    print(ros)
```



