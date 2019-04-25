# Ubuntu环境配置

#### SSH连接服务器

* #### **ssh user@ip -p 22**
* **ssh leva@172.16.207.129 -p 22**

---

### Mysql安装

* **安装mysql **`sudo apt-get install mysql-server`** **
* **登录mysql** `sudo mysql -u root -p`
* **创建用户**`create user 'leva'@'%' identified by 'leva123';`
* **用户赋予权限 **`grant all on *.* to 'leva'@'%';`
* **立即生效**`flush privileges;`

---

### **Python环境安装和配置**

**安装pip3**

```
sudo apt install python3-pip
```

**安装virtualenv和virutalenvwrapper**

Virtaulenvwrapper是virtualenv的扩展包，用于更方便管理虚拟环境，它可以方便实现以下功能：

* **将所有虚拟环境整合在一个目录下**
* **管理（新增，删除，复制）虚拟环境**
* **切换虚拟环境**

```
pip3 install virtualenv
pip3 install virtualenvwarpper
```

**配置**

此时还不能使用virtualenvwrapper，默认virtualenvwrapper安装在/usr/local/bin下面，实际上需要运行virtualenvwrapper.sh文件才行。修改~/.bashrc，添加以下语句

* **创建目录用来存放虚拟环境**

```
sudo mkdir $HOME/.virtualenvs
```

* **在~/.bashrc中添加行**

`vi ~/.bashrc`最后插入如下代码：

```
export WORKON_HOME=$HOME/.virtualenvs
export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3
export VIRTUALENVWRAPPER_VIRTUALENV=~/.local/bin/virtualenv
source ~/.local/bin/virtualenvwrapper.sh
```

* **运行**

```
source ~/.bashrc
```

* **创建项目运行环境**

```
mkvirtualenv 项目名称
mkvirtualenv tornado1
```

* **列出可用的项目运行环境**

```
workon 查看项目名称  
workon tornado1
```

* **退出项目环境**

```
deactivate
```

* **删除项目运行环境**

```
rmvirtualenv tor
```



