**文件可以持久存储，但是现在类似于临时的一些文件，不需要持久存储，如一些临时的二维码等，这个不需要持久存储，但是却需要短时间内大量读取，这是时候还是只能保存在文件里面吗？**

### StringIO

```py
创建IO操作:
    import io
    sio = io.StringIO()

写入:
    sio.write(str(i))

读取:
    sio.getvalue()

StringIO在内存中如同打开文件一样操作字符串，因此也有文件的很多方法
当创建的StringIO调用close()方法时，在内存中的数据会被丢失
--------------------------------------------------------
import io
sio = io.StringIO()
sio.write('hello')
print(sio.getvalue())
```

### BytesIO

```py
创建BytesIO:
    import io
    bio = io.BytesIO()

写入:
    bio.write(b'abcd')

读取:
    sio.getvalue()

BytesIO 和 StringIO 类似，但是BytesIO操作的是Bytes数据
--------------------------------------------------------

import io
bio = io.BytesIO()
bio.write(b'abc') #二进制写入
print(bio.getvalue())
```

### IO流总结

* **了解：**StringIO 和 BytesIO 的基本用法



