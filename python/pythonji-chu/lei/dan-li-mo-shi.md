**类每次实例话的时候都会创建一个新的对象，如果要求类只能被实例化一次改怎么做**

```py
class Earth:
    def __new__(cls):
        if not hasattr(cls,'instance'):
            cls.instance = super().__new__(cls)
        return cls.instance

    def __init__(self):
        self.name = 'earth'

e = Earth
print(e,id(e))

a = Earth
print(a,id(a))
```

在上面的例子中，我们可以看到两个实例的ID是相同的，意味着这里两个其实引用的是同一个实例，，是一个是的不同名字

**\_\_new\_\_方法**

* **初始化函数之前：**\_\_new\_\__ 方法会在初始化函数_\_\_init\_\_之前执行
* **单例模式：**利用这个\_\_new\__\_ \_可以很方便的实现类的单例模式
* **合理利用：**\_\_new\_\_方法合理利用可以带来方便，常应用在类的单例模式

### \_\_new\_\_方法总结

* **必须掌握：**\_\_new\_\_方法的运算顺序
* **了解：**使用\_\_new\_\_方法的单例模式应用



