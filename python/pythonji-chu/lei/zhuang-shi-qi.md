### 装饰器

* **他可以在不改变原有函数的基础上给函数增加一些新的功能**
* **不会影响你们之后写的代码，会，轻松很多**

```py
装饰器

def outer(func): #参数，函数体，用来完成一些新的功能
    def inner():
        print('---验证功能---')
        func()
    return inner #返回出来的是一个函数体
def func():
    print('---登录功能----')

func = outer(func) #装饰器写法还有一种简写方式
func()
_________________________________________________

装饰器简写@outer

def outer(func): #参数，函数体，用来完成一些新的功能
    def inner():
        print('---验证功能---')
        func()
    return inner #返回出来的是一个函数体

@outer  #装饰器简写
def func():
    print('---登录功能----')
func()
```

### 三个内置装饰器

```py
#property装饰器，就像访问属性一样
class Rectangle:
    def __init__(self,length,width):
        self.length = length
        self.width = width

    @property #就像访问属性一样
    def getArea(self):
        return self.length * self.width

a = Rectangle(20,20)
print(a.getArea)
_________________________________________________

@staticmethod #静态方法，不能访问类里面其他的类函数跟类方法一样
class Rectangle:
    def __init__(self,length,width):
        self.length = length
        self.width = width

    @staticmethod #静态方法
    def func():   #如果写了self，在调用时会报错
        print('staticmethod func')
Rectangle.func() #解绑，不需要实例可以调用类方法
_________________________________________________

@classmethod 类方法（会把类本身传进去），可以访问类属性跟类方法

class Rectangle:
    name = 'ceshi'
    def __init__(self,length,width):
        self.length = length
        self.width = width


    @classmethod
    def show(cls):
        print(cls.name)
        print('show fun')

Rectangle.show()
```

### 类装饰器

```py
class TestClass:
    def __init__(self,func):
        self.func = func

    def __call__(self, *args, **kwargs):
        print('--call--')
        return self.func()

@TestClass
def func():
    print('正在运行程序')

func()
```

**修饰函数：**修饰函数

**增加功能：**给函数增加功能

**内置装饰器：**三个内置装饰器是需要掌握的，在项目中会经常使用

### 装饰器总结

* **必须掌握：**装饰器概念和用法
* **必须掌握：**三个内置装饰器的方法

### 练习

测试type和isinstance两个函数，哪个速度更加的快

```py
from datetime import datetime

def run_time(func):
    def new_func(*args, **kwargs):
        start_time = datetime.now()
        print('程序开始时间%s' % start_time)
        func(*args, **kwargs)
        end_time = datetime.now()
        print('程序结束时间:%s' % end_time)
        print('程序总共执行时间:%s' % (end_time - start_time))
    return new_func
@run_time
def my_type():
    print('---type---')
    for i in range(10000):
        type('hello')

@run_time
def my_isinstance():
    print('---isinstance---')
    for i in range(10000):
        isinstance('hello',str)

my_type()
my_isinstance()
```



