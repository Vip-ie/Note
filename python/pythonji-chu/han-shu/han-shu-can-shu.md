### 函数参数

#### 函数里面可以传入那些对象

* **必备参数：**
  在函数调用的时候，必备参数必须要传
* **默认参数：**
  在调用参数的时候，默认参数可以不传入值，不传入值时，会使用默认参数
* **不定长参数：**
  在函数调用的时候，不定长参数可以不传入，也可以传入任意长度。其中定义时，元组形式可以放到参数最前面，字典形式只能放到最后面

**必备参数**

```py
def func(x):
    pass
```

**不定长参数**\(可以接受任意长度参数\)

```py
def func(*args,**kwargs):
    pass
参数的调用：
位置参数:*args传参数以元组方式接收
关键字参数:**kwargs传数以字典方式接收
-------------------------------------------------------
def func(*args):
    print(args)
func(1,2)

def func(*args):
    print(args)    
func(1,2,3,'a','b','c')

def func(**kwargs):
    print(kwargs)
func(a='b',c=18)

def func(*args,**kwargs):
    print(args,kwargs)
func(*(1,2,3,4),**{'name':'zlk','age':18})
```

**默认参数**

```py
默认参数，你可以传，如果传了按照你传的值执行，如果没有传按照默认的值执行。
def func(x,y=None):
        pass
def func(x,y=160):
        print('打印出我的升高差CM：')
        print('------开始-------')
        return x-y
xy =func(180)
print(xy)
```

`在python中参数无类型，参数可以接收任意对象，只有函数中代码才会对参数类型有限制`

### 函数参数总结

**必须掌握：**函数的三种参数的定义

**必须掌握：**每种参数的传参
