**如果在一个类中实例化另一个类，对这个属性进行访问的时候怎么做**

### 描述符

```py
class MyClass:
    def __get__(self, instance, owner):
        print("恭喜你获得了S级武器")

    def __set__(self,instance,value):
        print("this is %s" % value)

    def __delete__(self, instance):
        print("武器已经损坏")

class Control:
    attr = MyClass()

c = Control()
c.attr  #调用属性，会去我们的MyClass类里面执行__get__方法

c.attr = 20 #重新赋值
del(c.attr) #执行MyClass类里面执行__delete__方法
```

这类里面实例化另一个类，对这个实例作访问是，需要定义\_\_get\_\_ \_\_set\_\_ \_\_delete\_\_方法

### 魔法方法

* 描述符了解即可
* 魔术方法的作用其实是让开发人员能够更加灵活的控制类的表现形式

### 描述符

* 了解描述符即可



