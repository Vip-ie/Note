# UbuntuServer设置开机自启动

ubuntu-18.04不能像ubuntu14一样通过编辑rc.local来设置开机启动脚本，通过下列简单设置后，可以使rc.local重新发挥作用。

#### 1. 建立rc-local.service文件

```
sudo vi /etc/systemd/system/rc.local.service
```

#### 2. 将下列内容复制进rc-local.service文件

```
#  SPDX-License-Identifier: LGPL-2.1+
# 
#  This file is part of systemd.
#
#  systemd is free software; you can redistribute it and/or modify it
#  under the terms of the GNU Lesser General Public License as published by
#  the Free Software Foundation; either version 2.1 of the License, or
#  (at your option) any later version.

# This unit gets pulled automatically into multi-user.target by
# systemd-rc-local-generator if /etc/rc.local is executable.

[Unit]
Description=/etc/rc.local Compatibility
ConditionFileIsExecutable=/etc/rc.local

[Service]
Type=forking
ExecStart=/etc/rc.local start
TimeoutSec=0
StandardOutput=tty
RemainAfterExit=yes
SysVStartPriority=99

[Install]
WantedBy=multi-user.target
```

#### 3. 创建文件rc.local

```
sudo vi /etc/rc.local
```

#### 4. 将下列内容复制进rc.local文件

```
#!/bin/sh -e
#
# rc.local
#
# This script is executed at the end of each multiuser runlevel.
# Make sure that the script will "exit 0" on success or any other
# value on error.
#
# In order to enable or disable this script just change the execution
# bits.
#
# By default this script does nothing.
echo "看到这行字，说明添加自启动脚本成功。" > /usr/local/test.log
exit 0
```

#### 5. 给rc.local加上权限

```
sudo chmod +x /etc/rc.local
```

#### 6. 启用服务

```
sudo systemctl enable rc-local
```

#### 7. 启动服务并检查状态

```
sudo systemctl start rc-local.service
sudo systemctl status rc-local.service
```

#### 8. 创建软链接

做完这一步，还需要最后一步 前面我们说 systemd 默认读取 /etc/systemd/system 下的配置文件, 所以还需要在 /etc/systemd/system 目录下创建软链接

```
ln -s /lib/systemd/system/rc.local.service /etc/systemd/system/ 
```

#### 9. 重启并检查test.log文件

```
cat /usr/local/test.log
```



