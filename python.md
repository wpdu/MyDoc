# Python
## pip
- python -m pip install --upgrade pip       pip 升级
- python freeze > requirements.txt          到处当前所有pip包
- python install -r requirements.txt        安装所有pip包

## virtualenv
- virutalenv venv           创建venv虚拟环境
- venv/Scripts/activate     进入虚拟环境
- venv/Scripts/disactivate  退出虚拟环境


# vscode err
* venv/Scripts/activate 无法执行
    - 第一步：以管理员身份运行powershell
    - 第二步：执行：get-ExecutionPolicy 回复Restricted，表示状态是禁止的。
    - 第三步：执行：set-ExecutionPolicy RemoteSigned
    - 第四步：选择Y，回车


# pip
* pip install [name]==      查看所有版本
* pip show [name]           查看包信息


## 异常
- 弹窗执行 python 脚本      管理员打开powershell执行`Set-ExecutionPolicy RemoteSigned`
