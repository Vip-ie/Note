# 部署和运行

## 运行多个Tornado实例

* 网页响应不是特别的计算密集型处理
* 多个实例充分利用 CPU
* 多端口怎么处理
* Linux 常见应用服务配置模式 nginx 和 supervisord：采用**主配置文件 + 项目配置文件**

---

## 使用Supervisor监控Tornado进程

官方网址：[http://supervisord.org/](http://supervisord.org/)

### 安装Supervisor（如果用pip安装注意看是否需要指定使用python2版本）

supervisor默认只支持Python2

```bash
sudo apt-get install supervisor
```

或者激活Python3的vritualenv后执行，进入项目根目录安装支持Python3版本的supervisor

```
pip install git+https://github.com/Supervisor/supervisor.git
```

supervisor安装完成后，在项目根目录下有一个 `echo_supervisord_conf`文件

* 检查主配置文件 /etc/supervisor/supervisord.conf （如果在目录不存在需要创建）
* 使用命令生成一个**主服务配置文件** 项目目录执行`echo_supervisord_conf > deploy/supervisord.conf`（在项目根目录建立 deploy 建立）编辑deploy/supervisord.conf文件检查是否 inculde 配置，没有就加上

```
[include]
files = /super/*.conf #这里是添加的项目运行配置文件目录
```

如果 sudo 没有权限就用当前目录生成，然后

`sudo cp deploy/supervisord.conf /etc/supervisor/supervisord.conf`过去

* 在deploy目录下增加 Supervisor 项目运行配置文件（名字如 tornado1.ini）到 /etc/supervisor/conf.d

```
  ├── deploy
  │   ├── super
  │   │   └── tornado1.ini
  │   └── supervisord.conf
```

* tornado1.ini文件内如如下

```ini
# 增加一个tornadoes组
[group:tornadoes]
programs = tornado-8000,tornado-8001,tornado-8002

# 分别定义三个tornado的进程配置

[program:tornado-8000]
directory = /home/pyvip/ws/tudo28/ ; 程序的启动目录
command = /home/pyvip/.virtualenvs/tudo28/bin/python /home/pyvip/ws/tudo28/app.py --port=8000 ; 启动命令，与手动在命令行启动的命令是一样的，注意这里home不可用~代替
autostart = true     ; 在 supervisord 启动的时候也自动启动
startsecs = 5        ; 启动 5 秒后没有异常退出，就当作已经正常启动了
autorestart = true   ; 程序异常退出后自动重启
startretries = 3     ; 启动失败自动重试次数，默认是 3
user = pyvip         ; 用哪个用户启动
redirect_stderr = true  ; 把 stderr 重定向到 stdout，默认 false
stdout_logfile_maxbytes = 20MB  ; stdout 日志文件大小，默认 50MB
stdout_logfile_backups = 20     ; stdout 日志文件备份数
; stdout 日志文件，需要注意当指定目录不存在时无法正常启动，所以需要手动创建目录（supervisord 会自动创建日志文件）
stdout_logfile = /tmp/tornado_app_8000.log
loglevel = info

[program:tornado-8001]
directory = /home/pyvip/ws/tudo28/
command = /home/pyvip/.virtualenvs/tudo28/bin/python app.py --port=8001
autostart = true
startsecs = 5
autorestart = true
startretries = 3
user = pyvip
redirect_stderr = true
stdout_logfile_maxbytes = 20MB
stdout_logfile_backups = 20
stdout_logfile = /tmp/tornado_app_8001.log
loglevel = info

[program:tornado-8002]
directory = /home/pyvip/ws/tudo28/
command = /home/pyvip/.virtualenvs/tudo28/bin/python app.py --port=8002
autostart = true
startsecs = 5
autorestart = true
startretries = 3
user = pyvip
redirect_stderr = true
stdout_logfile_maxbytes = 20MB
stdout_logfile_backups = 20
stdout_logfile = /tmp/tornado_app_8002.log
loglevel = info
```

### 启动和管理

##### 启动supervisor

一定要先启动 daemon 程序 \(supervisord\) 才能执行管理操作，否则会报错

> 使用默认的主配置文件 /etc/supervisor/supervisord.conf
>
> **sudo supervisord**明确指定主配置文件sudo supervisord -c /home/pyvip/working/supervisord.conf
>
> 使用 user 用户启动supervisord
>
> sudo supervisord -u user

##### 查看、操作进程状态

> **\(tornado\) pyvip@Vip:~/ws/tudo$ sudo supervisorctl**
>
> \[sudo\] password for pyvip:
>
> tornadoes:tornado-8000 RUNNING pid 17652, uptime 0:00:28
>
> tornadoes:tornado-8001 RUNNING pid 17653, uptime 0:00:28
>
> tornadoes:tornado-8002 RUNNING pid 17654, uptime 0:00:28
>
> \#停止运行tornado-8001服务器进程
>
> supervisor&gt; stop tornadoes:tornado-8001
>
> tornados:tornado-8001: stopped
>
> \#停止运行整个tornado服务器进程组
>
> supervisor&gt; stop tornadoes:
>
> tornadoes:tornado-8000: stopped
>
> tornadoes:tornado-8001: stopped
>
> tornadoes:tornado-8002: stopped
>
> supervisor&gt; status
>
> tornadoes:tornado-8000 STOPPED Jun 26 07:43 PM
>
> tornadoes:tornado-8001 STOPPED Jun 26 07:43 PM
>
> tornadoes:tornado-8002 STOPPED Jun 26 07:43 PM

##### supervisorctl 命令介绍

> 停止某一个进程，program\_name 为 \[program:x\] 里的 x
>
> supervisorctl stop program\_name
>
> 启动某个进程
>
> supervisorctl start program\_name
>
> 重启某个进程
>
> supervisorctl restart program\_name
>
> 结束所有属于名为 groupworker 这个分组的进程 \(start，restart 同理\)
>
> supervisorctl stop groupworker:
>
> 结束 groupworker:name1 这个进程 \(start，restart 同理\)
>
> supervisorctl stop groupworker:name1
>
> 停止全部进程，注：start、restart、stop 都不会载入最新的配置文件
>
> supervisorctl stop all
>
> 载入最新的配置文件，停止原有进程并按新的配置启动、管理所有进程
>
> supervisorctl reload
>
> 根据最新的配置文件，启动新配置或有改动的进程，配置没有改动的进程不会受影响而重启
>
> supervisorctl update

---

### 安装和运行

* 安装`sudo apt-get install nginx`
* 检测配置文件正确可用 `sudo nginx -t`
* 运行 `sudo nginx`
* 修改或增加了配置文件后重启  `sudo nginx -s reload`

### nginx 配置文件

主配置文件是`/etc/nginx/nginx.conf`

**项目对应的配置文件放到**`/etc/nginx/conf.d/`**或者**`/etc/nginx/sites-enabled/`

比如 tudo\_nginx 文件

```
upstream tornadoes{
    server 127.0.0.1:8000;   # 本地访问，只用 127.0.0.1
    server 127.0.0.1:8001;
    server 127.0.0.1:8002;
}

proxy_next_upstream error;

server {
    listen 8888;   # 一般是 80
    server_name 127.0.0.1; # 根据实际情况填写对应ip

    location /{
        proxy_pass_header Server;
        proxy_set_header Host $http_host;
        proxy_redirect off;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Scheme $scheme;
        # 把请求方向代理传给tornado服务器，负载均衡
        proxy_pass http://tornadoes;
    }
}
```

### 常见问题

1. Linux 目录和文件的操作

2. 命令的输入 tab 键补全的操作

3. 按文档操作的顺序 （supervisord 没有启动的报错）

4. supervisor 的 web 管理界面

5. 配置文件修改定制应用的套路

6. nginx 配置解释，conf 文件的作用

7. vim 的使用和 sudo

8. 为什么要用 nginx



