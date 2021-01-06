# adb 命令

- adb server didn't ACK 异常
    1. 查看adb server端口 `adb nodaemon server`
    2. 查看占用端口进程pid `netstat -ano | findstr "5037"`
    3. 查询pid是哪个具体应用 `tasklist /fi "pid eq 774"`
    4. 干掉这个应用

- adb devices
- adb shell
- adb shell ipconfig    查看设备ip
- adb remount
- adb install apkname
- adb push <local_path> <remote_path>
- adb pull <remote_path> <local_path>
- adb logcat| -ie "abc"     实时过滤日志

- adb -s sn shell
- adb connect [ip:5555]     通过ip链接设备

## shell
- ping -c 4 <ip>            查看ip
- ifconfig wlan0            查看网络
- getprop |grep chip        查看芯片信息

### 时间同步
- adb shell date -s "20200701.110900"
- adb shell date MMDDhhmmYY.ss set      月天时分年.秒   hw设备设置时间
- adb shell settings put global auto_time 1     恢复自动时间

## 负责命令
- adb shell if [ ! -d "{path}" ]; then mkdir {path}; fi     如果路径不存在，则创建文件夹
- adb shell if [ -f "{path}" ]; then rm {path}; fi          如果路径存在，则删除
- adb shell "nohup {path} &"            后台运行某文件
- 重启设备
    1. adb -s [sn] reboot
    2. adb -s [sn] wait-for-device
    3. adb -s [sn] shell getprop sys.boot_completed     初始化完成时返回1，否则0