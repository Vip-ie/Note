
---

---

# Django ORM

* **Django的ORM简介**
* **数据库连接配置**
* **模型的创建与映射**
* **数据的增删改查**

---

## Django**的**ORM**系统的分析**

![](/assets/Django_Orm.png)

1. **ORM概念:对象关系映射（Object Relational Mapping,简称ORM）**
2. **ORM的优势:不用直接编写SQL代码，只需像操作对象一样从数据库操作数据**

---

## django**模型映射关系**![](/assets/Djang_Orm01.png)

1. **模型类必须都写在app下的models.py文件中。**
2. **模型如果需要映射到数据库,所在的app必须被安装。**
3. **一个数据表对应一个模型类,表中的字段,对应模型中的类属性。**

---

## **数据库的配置**

**在settings.py中配置DATABASES**

```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',  # 数据库引擎
        'NAME': 'mydb',                        # 数据库名称
        'USER': 'admin',                       # 链接数据库的用户名
        'PASSWORD': 'Root110qwe',              # 链接数据库的密码
        'HOST': '127.0.0.1',                   # mysql服务器的域名和ip地址
        'PORT': '3306',                        # mysql的一个端口号,默认是3306
        }
    }
```

## pymsql**数据库连接器的配置**

**在虚拟环境中安装pymysql**

```
pip install pymysql
```

**设置连接器为pymysql**

在主目录下的的\_\_init\_\_.py文件添加下面两句

```
import pymysql
pymysql.install_as_MySQLdb()
```

---

## 使用Django中的模型

**在app下面的models.py中创建django模型类**

```
from django.db import models

class User(models.Model):
    id = models.AutoField(primary_key=True) #主键可以省略，django会自动给我们加上
    name =models.CharField(max_length=30)
    age = models.ImageField()
```

---

## 将模型类映射到数据库

1. **首先执行下命令，要创建映射文件**

```
python manage.py makemigrations
```

**  2. 执行以下命令，将映射文件中的映射数据提交到数据库中 **

```
python manage.py migrate
```



