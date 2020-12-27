<!--
 * @Author: your name
 * @Date: 2019-10-27 20:08:09
 * @LastEditTime: 2020-03-01 21:25:52
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \Doc\linux.md
 -->
* 查看ip：ip addr

* ls -l
* ln -s dir1 dir2
* ps -ef | grep nginx   查看进程
* netstat -nap|grep 10010   查看10010端口占用
* kill -9 [pid]         杀进程
- ss -lntpd | grep :22  查看22端口被那个程序占用
- 查看进程运行文件位置： linux下进程运行后，进程信息存储在/proc/进程id 目录下面，进程id查看命令 ps -ef | grep 进程名，vi /proc/进程id/environ 搜索PWD字段，则是该进程运行所在目录
- ping -c 2 www.baidu.com

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