### 循环

```py
while条件成立true
重复执行莫一件事

语法规则:
while 判断语句
    循环体
注意缩进
----------------------------
i = 0
while i < 10:
    print(i)
    1 += 1

my_list = [1,3,5,6,7,8,9,40,50]
i = 0

while i < len(my_list):
    if my_list[i] > 20:
        print('%d大于20' % my_list[i])
    else:
        print('%d小于20' % my_list[i])
    i += 1

for i in range(21):
    i += 1
    if i %5 == 0:
        continue
        print(i)
    else:
        print('%d输出结束'%i)
```

**continue（跳出当次循环）**

```py
需求，想跳过下列列表内9这个元素继续循环执行
------------------------------------------


my_list = [1,3,5,6,7,8,9,40,50]
i = -1
while i < len(my_list) -1: #因为索引值是从0开始的，所以获取列表长度需要-1
    i += 1
    if my_list[i] == 9:
        continue
    print(my_list[i])

continue的用法:
for i in range(21):
    if i %5 == 0
        continue
    print(i)
    else:
        print('输出结束')
```

**break和else**

```py
终止循环
break的用法:
li = [1,2,3,4,5,6,7,8,9]
i = -1
while i < len(li)-1:
    i +=1
    if li[i] == 5:
        break
    else:
        print('%d判断语句'%li[i])
------------------------------------------

else的用法
li = [1,2,3,4,5,6,7,8,9]
i = 0
while i < len(li):
    print(True if li[i] > 5 else False)
    i += 1
else:
    print('判断结束')
```

### 注意的要点

**循环可以被终止：**

1. 通过continue跳过当次循环
2. 通过break终止循环

**else的执行条件：**

1. 只有在循环不是被break终止情况下才会执行else中的内容

### while的应用

**控制程序流程**

* 对于不同的条件，执行不同的代码

**break**

* break可以在没有终止条件的情况下结束循环

**else**

* else只有在循环被终止条件终止的情况下才会执行

---

## while总结

必须掌握：while的使用

必须掌握：break和continue的作用

了解：else的用法

### 迭代循环

对于刚才列表的例子，有没有加便捷的方法去除列表中的元素呢？

**for 迭代**

```py
语法规则:
for i in obj:
    循环体
注意缩进
——————————————————————————————————————

li = [1,5,6,9,3,2]
    for i in li:
        print(i)
```

**range**

```py
range的用法：
for i in range(21):
    print(i)
------------------------------------------------------


如何打印出1-20内的整数？
for i in range(1,21):
    print(i)
------------------------------------------------------


在上面的基础上增加条件，如果是5的倍数就跳过，不打印出来？
for i in range(1,21):
    if i %5 == 0:
        continue
    print(i)
------------------------------------------------------
在上面的基础上增加条件，如果是5的倍数就跳出循环
for i in range(1,21):
    if i %5 == 0:
        break
    print(i)
```

### 注意的要点

**for的用法：**

* for 后面需要接上可迭代对象
* for会一次取出可迭代对象中的元素

**continue的用法：**

* continue和break类似，但是continue不会被终止循环，而是结束本次循环，跳到下一次循环

### for的应用

**控制程序流程**

* 对于不同的条件，执行不同的代码

**continue**

* continue可以跳过本次循环，进入下次循环

**else**

* else只有在正常迭代结束，即不是被break终止的情况

## for总结

**必须掌握：**for的使用

**必须掌握：**continue的作用

**了解：**else的用法

