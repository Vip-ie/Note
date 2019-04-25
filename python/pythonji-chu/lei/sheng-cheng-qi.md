**我们如何自己实现一个可迭代对象**

* 在自定义的类中，要实现\_\__iter_\_\_ 魔术方法，该魔术方法，必须要返回一个迭代器（也需要自己实现）

**是否有更加有更加优雅的方式**

* 生成器

### 迭代器协议

```py
class Cycle:
    def __init__(self,elem,n):
        self.elem = elem
        self.n = n
    def __iter__(self):     #iter()函数会自动调用 方法
        elem = self.elem
        n = self.n

        class CycleIter:
            def __init__(self):
                self.count = 0
            def __next__(self): #next()函数会自动调用该 方法
                if self.count < n:
                    self.count += 1
                    return elem
                else:
                    raise StopIteration
            def __iter__(self):
                return self
        return CycleIter()   # 该方法 会返回一个 迭代器
```

#### 生成器与yield

* **特性一：**类似与函数的逻辑
* **特性二：**支持显式的 **暂停 **和** 恢复**
* **特性三：**隐式的支持**迭代协议**

```py
def cycle(elem,n):
    count = 0
    while True:
        if count < n:
            count += 1
            yield elem
        else:
            break
```

### 生成器语法

```py
                  返回这个对象
yield一个对象      暂停这个函数
                  等待下次next重新激活 

def my_gen():              #定义生成器，由next函数触发执行
    print('第一次执行')
    yield 1                #返回一个 1 并暂停函数
    print('第二次执行')
    yield 2                #返回一个 2 并暂停函数
    print('第三次执行')      #没有代码了，引发StopIteration异常

g = my_gen()
v1 = next(g) #输出：第一次执行
print(v1)    #输出：1
v2 = next(g) #输出：第二次执行
print(v2)    #输出：2
v3 = next(g) #输出：第三次执行，并抛出一个StopIteration异常
```

### 归纳总结

* **只需了解：**_生成器_与_迭代器_的区别

> 生成器，是python提供的一种非常简便的语法能让我们来自己写出迭代器  
> 注意！生成器，是一种特殊的迭代器

* **必须掌握：**yield语法的基本使用



