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

