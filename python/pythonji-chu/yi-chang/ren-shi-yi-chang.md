### 什么是异常

异常就是报错

### Python的异常结构（基于继承）

在Python中**所有的异常**都是**继承自BaseException**

分为四大类**:**

1. **SystemExit：Python退出异常**
2. **KeyboardInterrupt：键盘打断**
3. **GeneratorExit：生成器退出**
4. **Exception：普通异常（只会使用这部分的异常）**

### Python中那些异常

```py
常见异常举例
NameError:name 'a'  is not defined
SyntaxError:invalid syntax
TypeError:unsupported operand type(s) for -: 'init' and 'str'
```

### 错误回溯

### ![](/assets/error.png)

### 认识异常总结

**需要了解：**异常的层级关系

**必须掌握：**查找报错的原因

