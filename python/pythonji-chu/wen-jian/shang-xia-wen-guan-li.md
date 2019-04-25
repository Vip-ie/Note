**文件能够自动关闭吗？**

### with

```py
with open（r'/Users/zhanglikai/Desktop/test.txt','r') as f:
    print(f.read())

with能够自动关闭文件，不需要执行close方法
```

### 上下文管理底层方法重写**\_\_enter\_\_ 和 \_\_exit\_\_**

```py
import time

class RunTime:
    def __enter__(self):
        self.start_time = time.time()
        return self.start_time
    def __exit__(self,exc_type,exc_val,exc_tb):
        self.end_time = time.time()
        self.run_time =self.end_time - self.start_time
        print(self.run_time)

with RunTime() as a:
    print(a)
    for i in range(10000000):
        pass
```

**通过这两个方法可以方便的实现上下文管理**

**with会把 \_\_enter\_\_ 的返回值复制给as后的变量**

### 上下文管理

* **with **使用with打开文件，则文件不需要自己关闭，会自动的关闭
* **\_\_enter\_\_ **进入时需要执行的代码，相当于准备工作
* **\_\_exit\_\_** 退出时需要执行的代码，相当于收尾工作

### 上下文管理总结

* **必须掌握：**with的用法和特点
* **了解：**\_\_enter\_\_ \_\_exit\_\_



