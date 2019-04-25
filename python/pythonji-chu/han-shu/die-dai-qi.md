### 迭代是一个怎样的过程

就是一个一次从数据结构中拿出东西的过程

### 能否用更加低级的while来实现

可以的，但是，需要自己控制下标并获取对应的元素

```py
the_list = [5,4,3,2,1]
index = 0
var = None
while index < len(the_list):
    var = the_list[index]
    print(var)
    index += 1
```

### 可迭代对象与迭代器的区别

```py
          迭代

for 迭代变量 in 可迭代对象
    每次循环都会自动让
        “迭代变量”指向”下一个元素“

例
the_list = [5,4,3,2,1]
for index in the_list:
    print(index)
```

### 从可迭代对象生成一个迭代器

* **迭代器 = iter（可迭代对象）**
* **下一个值 = next（迭代器）**

### for实现原理

```py
itr = iter(the_list)
try:
    while True:
        var = next(itr)
        print(var)
except StopIteration:
    pass
```

### 归纳总结

* **只需了解：**for... in ...的运行机制
* **必须掌握：**iter、next两个内置函数的使用
* **能够区分：**可迭代对象与迭代器



