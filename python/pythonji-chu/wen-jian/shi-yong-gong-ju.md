**文件可以直接新建，但是现在如果需要创建文件夹和移动文件夹怎么办**

### OS操作系统交互

**os模块提供python和操作系统交互的接口**

```py
直接调用系统命令:
    os.system('ls')

通用路径操作:
    os.path
    os.path.join(r'/home/pyvip',r'pycase')

文件项目操作:
    os.mkdir('test') #创建一个文件夹
    os.rename('test','test1') #文件重命名

os提供了python和操作系统交互方式，只要是和操作系统相关，就可以尝试在os模块中找方法

--------------------------------------------------------------------

mkdir例：
os.mkdir(r'/Users/zhanglikai/Desktop/virtualenvs/ooo/test') #创建一个test文件夹
os.rename(r'/Users/zhanglikai/Desktop/virtualenvs/ooo/test',r'/Users/zhanglikai/Desktop/virtualenvs/ooo/TT')
#test文件夹重命名

路径拼接path.join
a = os.path.join(r'/Users/zhanglikai','Destktop')
print(a)
```

### shutil高级文件操作

**shutil模块提供了许多关于文件和文件集合的高级操作**

```py
移动文件:
    shutil.move

复制文件夹:
    shutil.copytree

删除文件夹:
    shutil.rmtree

--------------------------------------------------------------------   
移动文件例
shutil.move(r'/Users/zhanglikai/Desktop/virtualenvs/ooo/TT',r'/Users/zhanglikai/Desktop/virtualenvs/TT')
```

### 常用工具总结

* **必须掌握：**os.system os.path,join
* **了解：**os shutil



