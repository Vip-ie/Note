### 异常

* **try：**将可能会发生异常的代码放在try中，进行尝试性执行
* **except：**except用来捕获异常，并进行响应的处理
* **else和finally：**else在没有异常的时候会执行finally不管是否有异常，都会执行

### 异常通常会带来怎么样的问题

* **程序停止**

```py
基本的try   except
try:
    f = open('xxoo.py','r')
except:
    print('发生了异常')

try:
    x = 0
    y = 1/x
except:
    print('发生了异常')
______________________________________________________
捕获具体的异常
try:
    f = open('xxoo.py','r')
except FileNotFoundError:
    print('发生了异常')  #文件xxoo.py不存在时会打印

try:
    x = 0
    y = 1/x
except FileNoteFoundError: #不会捕获到ZeroDivisionError
    print('发生了异常')      #会不打印
#而是抛出ZeroDivisionError
______________________________________________________

捕获多种异常
try:
    f = open('xxoo.py','r')
except FileNotFoundError:
    print('请输入正确的文件路径') #打印
except ZeroDivisionError:
    print('分母不能为0') #不打印
except Exception:
    print('其他的普通异常') #不打印

try:
    x = 0
    y = 1/x
except FileNotFoundError:
    print('请输入争取的文件路径') #不打印
except ZeroDivisionError:
    print('分母不能为0') #不打印
except Exception:
    print('其他的普通异常') #不打印


try:
    raise TypeError('主动抛出的类型错误')    
except FileNotFoundError:
    print('请输入争取的文件路径') #不打印
except ZeroDivisionError:
    print('分母不能为0') #不打印
except Exception:
    print('其他的普通异常') #不打印

try:
    raise TypeError('主动抛出的类型错误')    
except FileNotFoundError:
    print('请输入争取的文件路径') #不打印
except ZeroDivisionError:
    print('分母不能为0') #不打印
except Exception as e:
    print(isinstance(e,TypeError)) #True
    print(e) #主动抛出的类型错误
```

### 关于**Exception**及其**子类**的解释

* **代码中会出现的异常都是Exception的子类，因此在except中只需要在最后加上Exception即可**
* **在抛出异常的过程中，会从上倒下一次对比异常，找到之后就不会在往后查找**

### 更加丰富的结构

```py
try:
    x = 0
except Exception:
    print('发生了普通异常') #不打印
else:
    print('没有发生异常') #打印
finally:
    print('怎么都会执行') #打印
```

### 异常处理总结

* **必须掌握：**异常的基本语法
* **能够区分：**finally和else的区别

### 我们如何放置这个问题，从而利用异常



