# UbuntuServer分辨率修改

**修改Ubuntu Server的分辨率，其实就是找到关键的文件，然后修改参数，重启一下，就可以看见效果了。**

#### 打开文件并修改参数

文件位置：/etc/default/grub

修改位置：GRUB\_CMDLINE\_LINUX = "vga=0x31A"

vga参数表

|  | 640x480 | 800x600 | 1024x768 | 1280x1024 |
| :--- | :--- | :--- | :--- | :--- |
| 256 | 0x301 | 0x303 | 0x305 | 0x307 |
| 32k | 0x310 | 0x313 | 0x316 | 0x319 |
| 64k | 0x311 | 0x314 | 0x317 | 0x31A |
| 16m | 0x312 | 0x315 | 0x318 | 0x31B |

执行命令：`sudo vi /etc/default/grub`

#### 更新修改后的文件

执行命令：`sudo update-grub`

#### 重启电脑

执行命令： `sudo reboot`

---

## Ubuntu 换国内源 中科大源 阿里源 163源 清华源

国内有很多Ubuntu的镜像源，包括阿里的、网易的，还有很多教育网的源，比如：清华源、中科大源。

我们这里以中科大的源为例讲解如何修改Ubuntu里面默认的源。

编辑`/etc/apt/sources.list`文件, 在文件最前面添加以下条目\(操作前请做好相应备份\)：

```
中科大源
deb https://mirrors.ustc.edu.cn/ubuntu/ bionic main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-security main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse
```

```
然后执行命令：
sudo apt-get update
sudo apt-get upgrade
```

#### 阿里源 {#阿里源}

```
deb http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse
```

#### 163源 {#163源}

```
deb http://mirrors.163.com/ubuntu/ bionic main restricted universe multiverse
deb http://mirrors.163.com/ubuntu/ bionic-security main restricted universe multiverse
deb http://mirrors.163.com/ubuntu/ bionic-updates main restricted universe multiverse
deb http://mirrors.163.com/ubuntu/ bionic-proposed main restricted universe multiverse
deb http://mirrors.163.com/ubuntu/ bionic-backports main restricted universe multiverse
```

#### 清华源 {#清华源}

```
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-security main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse
```



