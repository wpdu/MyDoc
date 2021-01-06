# Python

## setup.py
- python setup.py install       通过源码安装
- python setup.py develop       通过开发方式安装到本地，方便修改同步使用
- python setup.py sdist         制作source distribution(源码发布包), 保存在 dist/*.gz
- python setup.py dbdist_wheel  生成 .whl 包
- twine upload dist/*           上传包到pip服务（需要配置账号）

## pip
- pip install *.whl             本地安装
- pip install flask==           显示可用版本
- pip install flask             在线安装
- pip show flask                显示本地包信息
- pip list --outdate            查看可更新包
- pip install --upgrade flask   更新包
- python -m pip install --upgrade pip       pip 升级
- python freeze > requirements.txt          导处当前所有pip包
- python install -r requirements.txt        安装所有pip包

## pipreqs
- pipreqs [options] ./ ==encoding=utf8  目录依赖包导出到 requirements.txt
- options:
    - --use-local           只用本地信息，不查询pip服务器
    - --pypi-server <url>   使用指定pip服务器

## virtualenv
- pip install virtualvenv           安装
- virtualenv venv                   创建venv虚拟环境
- virtualenv -p python3.7.9 venv    创建3.7.9版本的虚拟环境
- venv/Scripts/activate             进入虚拟环境
- disactivate                       退出虚拟环境

## UML类图生成
1. 安装`graphviz`绘图工具，添加环境变量
2. 执行`dot -T`命令，测试`graphviz`是否正常安装
3. 安装包`pyreverse`包，`pylint` 已继承该模块
4. 执行生成命令
    - pyreverse -o png -p Pyreverse *.py    生成单个文件类图
    - pyreverse -o png -p Pyreverse dir/    生成整个文件夹类图
    - pyreverse -ASmy -o png -p _01 dir/    生成整个文件夹类图，包括依赖库和包
    - pyreverse -o dot op Pyreverse *.py    生成文件的类信息

## pyinstaller
- pyinstaller -F -w icon=abc.icon test.py
    - -F  -onefile  打包成一个exe
    - -D  -onedir   打包成一个文件夹
    - -w  -window   窗口应用
    - -c  -console  控制台应用
    - -d --debug all 调试模式，方便检查问题
    - -clearn       生成前清空缓存
    - --additional-hooks-dir=hooks      添加缺失的包
        - 手动添加hook文件，下面写入hook目录的python文件中
        ```python
        from PyInstaller.utils.hooks import collect_all
        datas, binaries, hiddenimports = collect_all('humanize')
        ```

## PyQt
- 设计工具 pyqt5_tools
    1. 工具路径： \Lib\site-packages\pyqt5_tools\Qt\bin\designer.exe
    2. ui路径： \Lib\site-packages\pyqt5_tools\Qt\bin\ui
    3. 转换 ui 文件转换成 py 文件
        - pyuic5 -o *.py *.ui

## gRPC
> [grpc python快速教程](http://tizi365.com/archives/400.html)
1. proto文件生成接口文件
    - python -m grpc_tools.protoc -I./ --python_out=. --grpc_python_out=. ./nearby_ocr.proto


## 异常
- 弹窗执行 python 脚本      管理员打开powershell执行`Set-ExecutionPolicy RemoteSigned`


# anaconda
## 虚拟环境
- 包下载地址配置文件 .condarc
```c
ssl_verify: true
proxy_servers:
http: *
https: *
channels:
* defaults
```
- conda update conda        更新
- conda create --name <env_name> <package_name>
    - 例：conda create -n python3 python=3.6.4 numpy pandas
    - 安装位置：/usrs/<user_name>/anaconda3/env/<env_name>
- activate <env_name>
- deactivate
- conda create -n <new_env_name> --clone <copied_env_name>  克隆环境
- conda remove -n <env_name> --all                          删除

## 包管理
- conda search --full-name <package_full_name>  精确查找
- conda search <str>                            模糊查找
- conda list
- conda install <package_name>
- conda install --name <env_name> <package_name>    指定虚拟环境安装
- conda remove <package_name>
- conda remove --name <env_name> <package_name>
- conda update --all
- conda update <package_name>