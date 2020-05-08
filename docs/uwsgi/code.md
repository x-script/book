

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
# 前面6个根据实际修改，其他的可以不用改 
 2 [uwsgi]
 3 # 项目目录
 4 chdir=/Users/wsl/App/dev/recovery/recovery
 5 # 设置日志目录
 6 daemonize=/Users/wsl/App/dev/recovery/uwsgi.log
 7 # 静态文件的配置，配合static_url使用，前面的static是static_url中的字段
 8 static-map = /static=/Users/wsl/App/dev/recovery/recovery/static
 9 # 指定项目的wsgi模块
10 module=recovery.wsgi
11 # 指定IP端口       
12 http=127.0.0.1:8888
13 # 指定sock的文件路径       
14 socket=/Users/wsl/App/dev/recovery/recovery/uwsgi.sock
15 # 指定pid文件
16 pidfile=/Users/wsl/App/dev/recovery/recovery/uwsgi.pid
17 # 启用主进程
18 master=true
19 # 进程个数       
20 workers=3
21 # 在每个worker而不是master中加载应用
22 lazy-apps=true 
23 # 每个进程最大的请求数
24 max-request = 1000
25 # 启动uwsgi的用户名和用户组
26 uid=root
27 gid=root
28 # 自动移除unix Socket和pid文件当服务停止的时候
29 vacuum=true
30 # 启用线程
31 enable-threads=true
32 # 设置自中断时间
33 harakiri=30
34 # 设置缓冲
35 post-buffering=4096
36 #设置在平滑的重启（直到接收到的请求处理完才重启）一个工作子进程中，等待这个工作结束的最长秒数。这个配置会使在平滑地重启工作子进程中，如果工作进程结束时间超过了8秒就会被强行结束（忽略之前已经接收到的请求而直接结束）
37 reload-mercy = 8
```



### 关闭

```
uwsgi --stop uwsgi.pid
```



### 测试 uWSGI

```
// test_uwsgi.py
def application(env, start_response):
    start_response('200 OK', [('Content-Type','text/html')])
    return [b"Hello World"]
```

```
uwsgi --http :8000 --wsgi-file test_uwsgi.py
```

访问 [http://localhost:8000](http://localhost:8000/)

> 访问失败：1. 端口未开放