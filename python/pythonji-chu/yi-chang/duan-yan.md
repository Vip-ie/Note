### 如何能在代码中强制要求一个条件满足

```py
a = 1
b = 2
assert a > b #条件满足运行，条件不满足抛出异常
__________________________________________________

def func(name):
    assert name == 'rave'  #条件满足运行，条件不满足抛出异常

func('rave')
```

### 是否有专门的语法来完成

```py
不使用断言：
if not false：
    raise Exception('条件不满足')
__________________________________________________

使用断言：
assert True  #不抛出异常
assert False #抛出异常
```

### assert总结

* **只需了解：**assert的使用

### 自定义异常类型

```py
class ZhengnengliangError(Exception):
    pass


def func(name):
    if name == '正能量':
        print('--正在登录某某网站--')
    else:
        raise ZhengnengliangError('你不是正能量同学，看不了富力湾站！！！！')

func('正能量')
__________________________________________________

class ZhengnengliangError(Exception):
    pass


def func(name):
    if name == '正能量':
        print('--正在登录某某网站--')
    else:
        raise ZhengnengliangError('你不是正能量同学，看不了富力湾站！！！！')



try:
    func('正能量1')

except ZhengnengliangError as e:
    print(e)
```



