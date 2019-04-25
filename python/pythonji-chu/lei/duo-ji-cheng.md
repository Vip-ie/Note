### 多继承

* **Mro **类在生成时会自动生成方法解析顺序，可以通过 类名.mro\(\)来查看
* **Super** 函数可以来调用福来的方法，使用super的好处在于即使父类的改变，那么也不需要更改类中的代码
* **Mixin** 是一种开发模式，给大家在今后的开发中提供一种思路

```py
class  Base():
    def play(self):
        print('这是A类')

class Cbase():
    def play(self):
        print('这是C类')


class Zbases(Cbase,Base): #多继承这里调用是从左往右调用
    pass

c = Zbases()
c.play()
```

### 重写覆盖父类方法

当子类继承父类之后，如果子类不想使用父类的方法，可以通过重写来覆盖父类的方法

```py
class  Base():
    def play(self):
        print('这是A类')

class Zbases(Base): 
    def play(self):
        print('重写覆盖父类'

c = Zbases()
c.play()
```

### 重写父类方法之后，如果又需要使用父类的方法

```py
方法一
class  Base():
    def play(self):
        print('这是A类')

class Zbases(Base):
    def play(self):
        Base.play(self) #调用父类 可以使用覆盖父类方法也可以使用父类方法
        print('覆盖父类')

c = Zbases()
c.play()

方法二（super）推荐
class  Base():
    def play(self):
        print('这是A类')

class Zbases(Base):
    def play(self):
        super().play() #自动找父类
        print('覆盖父类')

c = Zbases()
c.play()
```

### mro查看继承类关系

```py
class  Base():
    def play(self):
        print('这是A类')


class Zbases(Base):
    def play(self):
        super().play()
        print('覆盖父类')

c = Zbases()
print(Zbases.mro()) #查看类继承关系
```

### 多继承总结

**必须掌握：**super的用法

**了解：**多继承方法解析顺序

**了解：**Mixin开发模式

