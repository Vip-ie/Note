# SQLAlchemy 目录

### 1. ORM

### 2. SQLAlchemy连接数据库

### 3. Module

### 4. 增删改查

---

## ORM

**ORM全称Object Relational Mapping对象关系映射**

**通过ORM可以不用关心后台是使用的哪种数据库，只需要按照ORM所提供的语法规则去书写相应的代码，ORM就会自动的转换成对应对应数据库的SQL语句**



---

## SQLAlchemy连接数据库

1. 安装mysql
2. 安装python包：pymysql、sqlalchemy

创建一个module文件夹，在文件夹内创建connect.py文件

```py
from salalchemy import create_engine 导入模块

#连接数据库信息
HOSTNAME= '127.0.0.1'
PORT= '3306'
DATABASE = 'orm'
USERNAME = 'leva'
PASSWORD = 'leva123'

#数据库连接URL
Db_url = 'mysql+pymysql://{}:{}@{}:{}/{}?charset=utf8'.format(
    USERNAME,
    PASSWORD,
    HOSTNAME,
    PORT,
    DATABASE
)

#连接数据库
engine = create_engine(Db_url)

#测试连接
if __name__ == '__main__':
    connection =engine.connect()
    result = connection.execute('select 1')
    print(result.fetchone())
```

---

## Module

#### 通过SQLAlchemy提供的语法来声明表

| **\_\_tablename\_\_** | **数据库中的表名** |
| :--- | :--- |
| **Column：** | **用来创建表中的字段的一个方法** |
| **Integer：** | **整型，映射到数据库中的int类型** |
| **String：** | **字符串类型，映射到数据库中的varchar类型，使用时，需要提供一个字符串长度** |
| **DateTime：** | **时间类型** |
| **primary\_key** | **主键约束** |
| **autoincrement** | **自增长** |
| **Boolean** | **布尔函数** |
| **relationship** | 自动添加属性 backref 申明一个属性 uselist申明一个表一对多或一对一关系，True为一对多，False为一对一，cascade所有的可选字符串项。all，所有操作都会自动处理到关联对象上，save-update,关联对象自动添加到会话，delete，关联对象自动从会话中删除，delete-orphan，属性中去掉关联对象，则会话中会自动删除关联对象，merge，session.merge\(\)时会处理关联对象。refresh-expire，session，expire\(\)时会处理关联对象。expunge，session.expunge\(\)时会处理关联对象。 |
| **ForeignKey** | **外键约束** |

#### 创建Module的Base类

```py
from salalchemy import create_engine 导入模块
from sqlalchemy.ext.declarative import declarative_base 导入Base类模块

#连接数据库信息
HOSTNAME= '127.0.0.1'
PORT= '3306'
DATABASE = 'orm'
USERNAME = 'leva'
PASSWORD = 'leva123'

#数据库连接URL
Db_url = 'mysql+pymysql://{}:{}@{}:{}/{}?charset=utf8'.format(
USERNAME,
PASSWORD,
HOSTNAME,
PORT,
DATABASE
)

#连接数据库
engine = create_engine(Db_url)

Base = decalarative_base(engine)
```

1. **对象关系型映射，数据库中的表与python中的类相对应，创建的类必须继承自sqlalchemy中的基类。**
2. **使用declarative方法定义的映射类依据一个基类，这个基类是维系类和数据表关系的目录。**
3. **应用通常只需要有一个Base的实例。我们通过declarative\_base\(\)功能创建一个基类。**

#### 创建Module

创建一个module文件夹内，创建一个text\_user\_module.py文件

```py
from datetime import datetime   #导入时间模块
from sqlalchemy import Column, Integer, String, DateTime

class User(Base):
    __tablename__ ="user"
    id = Column(Integer, primary_key=True, autoincrement=True)
    username = Column(String(20))
    password = Column(String(20))
    create_time = Column(DateTime, default=datetime.now())
    _locked = Column(Boolean, default=False, nullable=False)

    def __repr__(self):

#执行此代码，就会把创建好的 Module 映射到数据库中
if __name__ =="__main__":
    Base.metadata.create_all()
```

* **再次强调，我们用类来表示数据库里面的表！！！**
* **这些表的类都继承于我们的Base基类。**
* **在类里面我们定义一些属性，这个属性通过映射，就对应表里面的字段增删改查**

---

## 增删改查

**在对表数据进行增删改查之前，先需要建立会话，建立会话之后才能进行操作，就类似于文件要打开之后才能对文件内容操作**

#### 创建一个数据库连接connect.py文件

```py
from sqlalchemy import create_engine #导入sqlalchemy数据连模块
from sqlalchemy.ext.declarative import declarative_base  #引入Base类才可以创建基类
from sqlalchemy.orm import sessionmaker #导入会话模块

#连接数据库信息
HOSTNAME= '127.0.0.1'
PORT= '3306'
DATABASE = 'orm'
USERNAME = 'leva'
PASSWORD = 'leva123'

#数据库连接URL
Db_url = 'mysql+pymysql://{}:{}@{}:{}/{}?charset=utf8'.format(
    USERNAME,
    PASSWORD,
    HOSTNAME,
    PORT,
    DATABASE
)

#连接数据库
engine = create_engine(Db_url)
Base = decalarative_base(engine) #创建一个Base基类

Session= sessionmaker(engine) #创建一个实例会话
session = Session() #实例化一个对象
```

#### 创建一个数据库模型user\_modules.py文件

```py
from connect import Base     #导入Base基类
from datetime import datetime   #导入时间模块
from sqlalchemy import Column, Integer, String, DateTime, Boolean #导入sqlalchemy数据库映射模块



class User(Base):
    """建立数据库模型对应User表"""
    __tablename__ ='user'
    id = Column(Integer, primary_key=True, autoincrement= True)
    username = Column(String(20))
    password = Column(String(20))
    create_time = Column(DateTime, default=datetime.now())
    _locked = Column(Boolean, default=False, nullable=False)

#字符格式化显示
    def __repr__(self):
        return "<User(id=%s),username=%s,password=%s,create_time=%s, _locked=%s>"%(
            self.id,
            self.username,
            self.password,
            self.create_time,
            self._locked
        )
#执行以下命令创建一个数据库表
  if __name__ == '__main__':
     Base.metadata.create_all()
```

#### 创建一个text\_user\_modules.py文件用于处理数据库增删改查

```py
from connect import session #导入一个会话模块
from user_modules import User #导入一个数据库模型模块

def add_user():
    """添加数据单条数据"""
    preson = User(username='zlk',password='123')
    session.add(preson)
    """添加多条数据"""
    session.add_all([
        User(username='vip',password='123'),
        User(username='vip1',password='abc')
    ])
    session.commint() #提交数据库

def search_user():
    “”“查询数据”“”
    rows = session.query(User).all() #查找User数据模型内所有数据
    row = session.query(User).first() #查询User数据模型内第一条数据
    print(rows)

def update_user():
    session.query(User).filter(User.username=='zlk').update({User.password:1})
    #查找出用户名为zlk，然后update把这条数据的密码进行更新 .filter按条件查询
    session.commit()

def delete_user():
    """删除指定条件下数据"""
    rows = session.query(User).filter(User.username=='zlk')[0]   #[0]下标第一个符合条件
    print(rows)
    session.delete(rows)
    session.commit()


if __name__ =="__main__":
    # add_user() #添加数据
    # search_user() #查询数据
    # update_user()
    delete_user()
```

#### **query就是查询的意思，在SQLAlchemy中也用来查询数据**

* **all是查询所有的意思**
* **first是查询第一条数据**

```
rows = session.query(User).all()
rows = session.query(User).first()
```

#### **update更新数据**

```py
rows = session.query(User).filter(User.username=='zlk').update({User.password:1})
 session.commit()
```

#### Delete删除数据

```
rows = session.query(User).filter(User.username=='budong')[0] 
print(rows) 
session.delete(rows) 
session.commit()
```



