## kernel
- uname -r      查看核心版本

## linux distributions规范
- LBS           Linum Standard Base
- FHS           File system Hierarchy Standard

## 网络
* ip addr                   查看ip
* netcfg                    查看ip， wlan0
* ping -c 2 www.baidu.com   ping命令

## 文件
* ls -l
* ln -s dir1 dir2
* rm [-fir]         删除
* mv [-fiu]         移动，改名
* ps                查看运行的进程
* ps -x [pid]       查看进程状态
* top               查看那个进程占用率高
* su                切换到root用户
* chmod 777 <file>  修改文件权限


## 进程相关
* ps -ef | grep nginx       查看进程pid
* ps aux 与 ps -ef          两者功能一样，结构不太一样
* netstat -nap|grep pid     查看pid进程端口占用
* ss -lntpd | grep :22      查看22端口被那个程序占用
* kill -9 [pid]             杀进程
* 查看进程运行文件位置： linux下进程运行后，进程信息存储在/proc/进程id 目录下面，进程id查看命令 ps -ef | grep 进程名，vi /proc/进程id/environ 搜索PWD字段，则是该进程运行所在目录
* cd /proc/{pid}/fd
    - ls | wc -w            显示pid进程下当前fd数量
    - ls -l                 显示pid进程下所有fd
* cd /proc/{pid}/
    - cat limits            显示pid进程允许最大fd数量

# Ubuntu 包管理
## 在线
- apt-get install packagename
- apt-get remove packagename
- apt-cache search packagename
- apt-get update                修改 /etc/apt/sources.list 文件后更新包列表
- apt-get upgrade               升级本地安装包

## 源码安装
1. apt-get install build-essential  安装编译器
2. 下载源码，解压，进入目录
3. ./configure --prefix=/usr/local/webserver/nginx      扫描系统，必要库已存在，配置安装路径
4. make                             编译
5. make install                     安装到 /usr/local 目录
6. make uninstall                   卸载
7. dpkg -i package.deb              安装包

# Red Hat CentOS 包管理
- yum [options] [command] [packagename] 在线
- rpm -qi *.rpm                         本地 默认 rmp 格式

## 解压
- xz -d filename.tar.xz        xz文件解压
- gzip -d filename.tar.gz      gz文件解压
- tar -xvf filename            释放 tar

## 压缩
- tar -cvf filename             打包
- gzip -cvf filename            压缩成 .gz
- xz -z filename                压缩成 .xz

## 预览文件
- tail -n 10 <file>    显示最后10行
- tail -n +10 <file>   显示10行后所有
- head -n 10 <file>    显示前10行
- cat <file>           预览所有

## java环境变量
- whereis java      查找java安装路径
- which java        查看java执行路径
- echo $JAVA_HOME   查看环境变量
- echo $PATH
- 编辑 /etc/profile 全局环境变量
    - `vim /etc/profile`    进入编辑
    - 输入 export JAVA_HOME=/usr/share/jdk1.8.0
    - 输入 export PATH=$JAVA_HOME/bin:$PATH
    - 输入 export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
- 编辑 .bash_profile 修改个人环境变量
- 卸载 进入jdk安装目录下 uninst目录，再shell执行 ./uninstall.sh

## vim
1. vim filename         进入命令
2. i                    开始编辑
3. Esc                  退出编辑
4. ：                   底线命令模式
5. wq                   保存退出


* 后台运行命令：
    * unhup python3 app.py (> result.log )&
    * 编写 .sh 脚本
        1. 编写脚本
        2. 修改可执行权限 chmod +x filename
        3. 运行：./run.sh > result.log &
        4. 查看后台进程 ps -e

* 修改root权限：
    * CentOs/Fedora: su - root
    * Ununtu: sudo su -root
* 修改文件为可执行(*Permission denied 问题）： chmod u+x *.sh
* 将日志输出到控制台： cat result.log | more