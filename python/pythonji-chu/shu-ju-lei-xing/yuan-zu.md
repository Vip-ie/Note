### 元组定义

定义个元素，变量用小括号或无括号包裹起来，元素与元素之间用逗号隔开，元素是有序的、通过索引可以获取元素。

```py
>>>a_tuple = (1,2,'a','b') 
>>>a_tuple1 = 1,2,3,'aa','bb'
```

### 元组方法

```py
元组是不可变的，用在对数据安全性要求高的需求方面。
元组的使用方法和列表使用方法一样。
查：
    count  统计指定元素出现次数
    index  查看指定元素下标值

--------------------------------------------

>>> tup ='a','b','c','d'
--------------------------------------------

统计count
>>> tup.count('a')
1
--------------------------------------------

>>> tup.index('c')
2
```

### 元组的应用

元组是不可变对象，如果需要改变，转化成列表即可

元组中只有 count 和 index 方法，方便查找元组中的数据
