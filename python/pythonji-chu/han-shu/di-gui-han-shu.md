### 递归函数

```py
阶乘：
def factorial(n):
    if n == 1:
        return 1
    return factorial(n-1)*n

递归中可以函数自身调用自身，但是使用时类似于条件循环一样，要有递归的终止条件。
```

### 递归应用

使用递归时，常常可以让代码更加简洁

递归会占用比较多的内存，当递归次数比较多时，性能就会降低，因此不建议多使用递归。

### 递归总结

**必须掌握：**递归函数的定义

**熟悉递归函数的使用**
