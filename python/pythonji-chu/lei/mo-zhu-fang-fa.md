### 魔法方法之运算符

| 方法 | 描述 |
| :--- | :--- |
| \_\_add\_\_\(self,other\) | x + y |
| \_\_sub\_\_\(self,other\) | x - y |
| \_\_mul\_\_\(self,other\) | x\* y |
| \_\_mod\_\_\(self,other\) | x % y |
| \_\_iadd\_\_\(self,other\) | x += y |
| \_\_isub\_\_\(self,other\) | x -=y |
| \_\_radd\_\_\(self,other\) | y + x |
| \_\_rsub\_\_\(self,other\) | y - x |
| \_\_imul\_\_\(self,other\) | x \*=y |
| \_\_imod\_\_\(self,other\) | x %=y |

运算方法大家了解即可，在实际中应用并不多

```py
add两个数相加

class Rectangle:

    def __init__(self,length,width):
        self.length = length
        self.width  = width

    def area(self):
        areas = self.length * self.width
        return areas

    def __add__(self, other):
        add_length = self.length + other.length
        add_width  = self.width + other.width
        return add_length,add_width

a = Rectangle(3, 4)
b = Rectangle(5, 6)
print(a + b)
```

### str和repr原理

```py
class Rectangle:

    def __init__(self, length, width):
        self.length = length
        self.width = width

    def area(self):
        areas = self.length * self.width
        return areas

    def __str__(self):
        return 'length is %s, width is %s ' % (self.length, self.width)

    def __repr__(self):
        return 'area  is %s' % self.area()

p = Rectangle(20,30)

print(p)
```

**在python中，str和repr方法在处理对象的时候，分别调用的是对象的\_\_str\_\_ 和 \_\_repr\_\_方法print也是如此，调用str函数来处理输出的对象，如果对象没有定义\_\_str\_\_方法，则调用repr处理在shell模式下，展示对象\_\_repr\_\_的返回值**

* 对使**用者使用**友好的\_\_str\_\_
* 对开**发者调**试友好的\_\_repr\_\_

### \_\_call\_\_方法 实例进行调用

```py
class Rectangle:

    def __init__(self,length,width):
        self.length = length
        self.width  = width

    def area(self):
        areas = self.length * self.width
        return areas

    def __call__(self):

        return 'this is  __call__'

a = Rectangle(10,20)
print(a())
```

**正常情况下，实例是不能像函数一样被调用的，要想实例能够被调用，就需要定义 \_\_call\_\_ 方法**

### 魔法方法总结

**必须掌握：**\_\_str\_\__ _\_\_repr\_\_ \_\_call\_\_

**了解：**魔术方法的原理和作用

