### 匿名函数

```py
匿名函数的定义

lambda 参数：表达式
函数比较简单的情况下，用匿名函数的形式写，一眼就能看出来，增加代码的可读性
----------------------------------------
过滤一个列表内小于5的所有元素g
li = [3,20,5,7,18]
a = list(filter(lambda x: x>5,li))
print(a)

匿名函数的黑科技用法
g = lambda a : a >= 60
print(g(5))
print(g(70))
```

### 匿名函数的应用场景

**简单函数：**简单的函数，可以不用使用def定义一个函数，使用匿名函数即可

**函数调用：**类似与filter，map等函数里面，可以使用匿名函数来做处理

**投稿开发效率：**匿名函数的合理利用能够让哪个代码更加简介

### 匿名函数总结

**必须掌握：**匿名函数的用法

熟悉匿名函数的使用

