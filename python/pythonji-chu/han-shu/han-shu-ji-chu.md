### 函数基础

**函数定义**

```py
def 函数名（参数）:
    pass
    return 表达式

函数命命名规则：字母、数字和下划线组成、和变量命名规则一致
return 后面可以返回任意表达式，但不能是赋值语句
-------------------------------------------------------

例:
def func ():
    return True
a = func ()
print(a)
```

**return**

注意return和print的区别，return是函数的返回值，返回值可以复制给变量，而print只是打印出来

```py
def func (): 
    print("计算身高差")
    print('-----开始执行-----')
    return 3 +2      #return表示这个函数已执行完，函数后面的代码都不会被执
c = func ()
print(c)
```

**函数调用**

```py
def func (a,b):   #函数调用
    print("计算身高差")
    print('-----开始执行-----')
    return a-b 
    print('代码不执行')
num1 = int(input('请输入您的升高CM:'))
num2 = int(input('请输入其他人升高CM'))
c = func (num1,num2)
print(c)
```

### 函数基础总结

**必须掌握：**函数定义

**必须掌握：**return的用法

**必须掌握：**函数的调用

