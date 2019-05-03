# 部署和运行

## 运行多个Tornado实例

* 网页响应不是特别的计算密集型处理
* 多个实例充分利用 CPU
* 多端口怎么处理
* Linux 常见应用服务配置模式 nginx 和 supervisord：采用**主配置文件 + 项目配置文件**

---

## 使用Supervisor监控Tornado进程

### 安装Supervisor（如果用pip安装注意看是否需要指定使用python2版本）

```bash
sudo apt-get install supervisor
```



