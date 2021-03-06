### 函数作用域

在函数里面也可以定义变量，那函数里面的变量名如果和函数外面的变量重名，会互相影响吗？

答案是：不会受到影响

```py
a = 100
def func():
    a = 200
    print(a)
func()
print(a)
```

```py
作用域定义
命名空间，就是对一个名字起作用的范围，当前空间有效，
----------------------------------------------------------------
a=  100           #全局变量
def func():
    global a      #声明全局变量，你是全局变量，我要修改你
    a = 200       #局部变量只在函数内部生效（如果没有局部变量直接找函数外部变量）
    print(a)
    #return       #函数内如果不设置return 返回值，默认返回return None
func（）
print（a）
----------------------------------------------------------------

def func():
    a = 200
    def func1():
        nonlocal a #函数嵌套立即免想要改变这个局部变量（改变局部变量用nonlocal）
        a +=1
        return a
    return func1()
a = func()
print(a)
```

* **函数内部：**
  函数内部的变量，作用域只在函数内部，函数内部不可以直接更改函数外部的变量
* **global：**
  函数内部如果需要改变全局变量，就需要使用global修饰变量
* **nonlocal：**
  在函数嵌套函数的情况下，同样也有函数作用域的问题，但是python3中提供了方法，只需要使用nonlocal就可以在里层函数内部修改外部函数变量

### 函数作用域总结

**必须掌握：**全局变量和局部变量的概念

**必须掌握：**global，了解nonlocal

