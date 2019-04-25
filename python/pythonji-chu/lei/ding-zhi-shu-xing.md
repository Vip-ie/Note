**如何判断一个实例里面有某一个属性**

1. **怎么删除实例属性**
2. **怎么删除变量**

### 定制属性访问

![](/assets/length.png)

* **hasattr：**判断是否存在属性，如果属性存在则进行下一步操作
* **getattr：**得到属性值
* **setattr：**设置属性

```py
查:
    hasattr(re,'length')         #返回bool值
    getattr(re,'length;)         #返回属性值
    re.__getattribute__('length')#底层魔法方法

改:
    setattr(b,'length',6)        #改re对象length属性值为6
    re.__setattr__('length',5)   #底层魔法方法


增:
    re.aaa = 1                   #增加re对象一个aaa属性
    setattr(re,'bbb',2)          #re对象有bbb属性则改值无则增加bbb属性
    re.__setattr__('ccc',3)      #底层魔法方法

删: 
    delattr（re,‘ccc'）           #删除re对象一个ccc属性
    re.__delattr__('bbb')        #底层魔法方法
    del b
_________________________________________________________________

查例：
class Rectangle:
    def __init__(self,length,width):
        self.length = length
        self.width = width

    def getAttr(self):
        arrt = self.length * self.width
        return '面积:%d' % arrt

re = Rectangle(3,4)

print(hasattr(re,'length'))          #判断有没有这个属性
print(getattr(re,'length'))          #返回属性值
print(re.__getattribute__('length')) #底层__getattribute__魔法方法
_________________________________________________________________

改例：
class Rectangle:
    def __init__(self,length,width):
        self.length = length
        self.width = width

    def getAttr(self):
        arrt = self.length * self.width
        return '面积:%d' % arrt

re = Rectangle(3,4)
print(getattr(re,'length'))
print(re,'length',6)                #改re对象的length属性值为6
print(getattr(re,'length'))
_________________________________________________________________

增例:
class Rectangle:
    def __init__(self,length,width):
        self.length = length
        self.width = width

    def getAttr(self):
        arrt = self.length * self.width
        return '面积:%d' % arrt

re = Rectangle(3,4)

re.aaa = 'Rave'                    #re对象增加一个aaa属性并赋值为Rave
setattr(re,'bbb',18)               #re对象有bbb属性则改值无则增加bbb属性
print(getattr(re,'bbb'))
_________________________________________________________________

删例:
class Rectangle:
    def __init__(self,length,width):
        self.length = length
        self.width = width

    def getAttr(self):
        arrt = self.length * self.width
        return '面积:%d' % arrt

re = Rectangle(3,4)

delattr(re,'length')             #re对象length属性删除
print(hasattr(re,'length'))
del re                           #删除re变量
```

### 定制属性访问总结

* **必须掌握：**hasattr、getattr、setattr
* **了解：**\_\_getattribute\_\_
* **熟悉：**属性调用规则



