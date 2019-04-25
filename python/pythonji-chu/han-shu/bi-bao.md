### 闭包

**闭包定义**

```py
函数里面再定义一个函数，并且外层函数返回了内存函数的函数体
函数里面再定义一个函数，这个函数用到了外面这个函数变量。
-------------------------------------------------
def func():
    def func1():
        print('这是一个内层函数')
        return 3
    return func1     #返回一个func1 函数体，函数对象
a = func()
print(a())



def func(num):
    def func1(num_in):
        return num + num_in
    return func1
c =func(100)
print(c(130))
```



