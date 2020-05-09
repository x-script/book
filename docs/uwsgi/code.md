

### 启动

##### 启动方式1：命令行启动

> & 后台运行不占用终端窗口

```
uwsgi --http 127.0.0.1:8000 --wsgi-file test_uwsgi.py &
```



##### 启动方式2：配置文件启动(推荐)

```
uwsgi --ini uwsgi.ini
```

```
# uwsgi.ini

[uwsgi]
# http=127.0.0.1:8000
socket=127.0.0.1:8000
# 项目目录
chdir=/home/test_api
# 项目中 wsgi.py 文件的目录，相对于项目目录
wsgi-file=test_api/wsgi.py
# 指定启动的工作进程数
processes=4
# 指定工作进程中的线程数
threads=2
# 启用主进程
master=True
# 保存启动之后主进程的 pid
pidfile=uwsgi.pid
# 设置 uwsgi 后台运行，uwsgi.log保存日志信息
daemonize=uwsgi.log
```



### 关闭

```
uwsgi --stop uwsgi.pid
```



### 测试  uWSGI

```
# test_uwsgi.py
# 函数 application
def application(env, start_response):
    start_response('200 OK', [('Content-Type','text/html')])
    return [b"Hello World"]
```

```
uwsgi --http :8000 --wsgi-file test_uwsgi.py
```

访问 [http://localhost:8000](http://localhost:8000/)

> 访问失败：1. 端口未开放