### 继承

类的继承子类继承

```py
class Rectangle:  # 矩形类
    def __init__(self,length,width):
        self.length = length
        self.width  = width

    def area(self):
        areas = self.length * self.width
        return areas

class  jicheng(Rectangle): #继承父类方法
    pass

p =jicheng(10,20)
print(p.area())  #调用父类属性
```

父类与子类是同一块空间吗

```py
class fulei:
    name = 'aaa'

class zilei(fulei):
    pass

print(id(fulei))
print(id(zilei))
140666839506040
140666839580312  #两个ID不一样就能判断出是不是同一空间
```

### 重用父类的\_\_init\_\_

```py
class Rectangle:  # 矩形类
    def __init__(self,length,width):
        self.length = length
        self.width  = width

    def area(self):
        areas = self.length * self.width
        return areas

class  Square(Rectangle):
    def __init__(self,length,width)
        if lenth == width:
            Rectangle.__init__(self,length,width)
```

### 继承总结

**必须掌握：**继承的概念和使用方法

**了解：**继承搜索

**了解：**object 基类

