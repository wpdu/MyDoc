# Flask_Deploy

## 安装环境

## git
1. 安装
    * cat /etc/*release*        查看系统信息
    * sudo yum install git -y   CentOS 安装
    * apt-get install git -y    Ununtu/Debin 安装  
    * git --version             查看结果
2. 配置
    * git config --global user.name "wpdu"
    * git config --global user.email "duyanjie_1@163.com"
    * mkdir ./.ssh/     创建sshkey 目录
    * cd .ssh
    * ssh-keygen -t rsa -C "duyanjie_1@163.com"
    * yum install vim   安装vim
    * vim id_rsa.pub
    * 拷贝 pubkey 到github账户
    * Esc -> :q         退出vim
    * git clone git@github.com:wpdu/Switcher.git   克隆源码
## python pip


## uwsgi (已被gunicorn替换)
1. 默认配置 ~/.uwsgi/uwsgi.ini  (路径没有限制)
    [uwsgi]
    http=127.0.0.1:8888
    wsgi-file=/home/ubuntu/flask_test/app.py
    callable=app
    processes=4
    threads=2
    stats=127.0.0.1:9191
    touch-reload=/home/ubuntu/flask_test
2. 启动服务
    uwsgi --ini /.uwsgi/uwsgi.ini
3. 持续坚挺配置变化：
    将配置文件放到该路径下, 或者进行软连接 ln -s src tag
    uwsgi --emeror /.uwsgi/vassals/     开始监听
4. 放在后台持续运行
    nohup uwsgi --emperor /.uwsgi/vassals/ &

## gunicorn
>Gunicorn (独角兽)是一个高效的Python WSGI Server,通常用它来运行 wsgi application(由我们自己编写遵循WSGI application的编写规范) 或者 wsgi framework(如Django,Paster),地位相当于Java中的Tomcat。 WSGI就是这样的一个协议：它是一个Python程序和用户请求之间的接口。WSGI服务器的作用就是接受并分析用户的请求，调用相应的python对象完成对请求的处理，然后返回相应的结果。 简单来说gunicorn封装了HTTP的底层实现，我们通过gunicorn启动服务，用户请求与服务相应都经过gunicorn传输

1. 虚拟环境
    * mkdir venv
    * python -m venv venv   创建
    * source venv/bin/activate    激活
    * deactivate    退出
2. 安装依赖
    * pip install -r requirements.txt
3. 安装gunicorn
    * pip install gunicorn
    * 创建 wsgi.py 文件
```python
    from app import create_app
    application = create_app('production')
    if __name__ == '__main__':
        application.run()
```
4. 启动 gunicorn -w 4 -b 0.0.0.0:10000 app:appl

## 安装Nginx
>nginx 是一个高性能的web服务器。通常用来在前端做反向代理服务器。所谓正向与反向（reverse），只是英文说法翻译。代理服务，简而言之，一个请求经过代理服务器从局域网发出，然后到达互联网上服务器，这个过程的代理为正向代理。如果一个请求，从互联网过来，先进入代理服务器，再由代理服务器转发给局域网的目标服务器，这个时候，代理服务器为反向代理（相对正向而言）。
* 正向代理：{ 客户端 ---》 代理服务器 } ---》 服务器
* 反向代理：客户端 ---》 { 代理服务器 ---》 服务器 }
* {} 表示局域网

0. CentOS7 默认没有提供 Nginx 的源，但 Nginx 自己提供了
    > sudo rpm -Uvh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm
1. 启动：yum -y install nginx
2. 停止：service nginx stop
3. 重启：service nginx restart
3. 平滑重启：nginx -s reload
5. 配置文件路径：/etc/nginx/nginx.conf

## 

***

### 引用
[CentOs](https://blog.csdn.net/qq_35304570/article/details/80304482)  
[Python安装](https://blog.csdn.net/qq_35304570/article/details/80302872)