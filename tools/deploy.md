# 部署和运行

## 运行多个Tornado实例

* 网页响应不是特别的计算密集型处理
* 多个实例充分利用 CPU
* 多端口怎么处理
* Linux 常见应用服务配置模式 nginx 和 supervisord：采用**主配置文件 + 项目配置文件**

---

## 使用Supervisor监控Tornado进程

### 安装Supervisor（如果用pip安装注意看是否需要指定使用python2版本）

supervisor默认只支持Python2

```bash
sudo apt-get install supervisor
```

或者激活Python3的vritualenv后执行，安装支持Python3版本的supervisor

```
pip install git+https://github.com/Supervisor/supervisor.git
```

* 检查主配置文件 /etc/supervisor/supervisord.conf （如果目录不存在需要创建）
* 使用命令生成一个**主服务配置文件**`echo_supervisord_conf > deploy/supervisord.conf`（如果没有 deploy 目录就建立）

检查是否 inculde 配置，没有就加上

```
[include]
files = /etc/supervisor/conf.d/*.conf
```

如果 sudo 没有权限就用当前目录生成，然后

`sudo cp deploy/supervisord.conf /etc/supervisor/supervisord.conf`过去

* 增加 Supervisor 项目运行配置文件（名字如 tudo\_super.conf）到 /etc/supervisor/conf.d

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



