# vscode err
* venv/Scripts/activate 无法执行
    - 第一步：以管理员身份运行powershell
    - 第二步：执行：get-ExecutionPolicy 回复Restricted，表示状态是禁止的。
    - 第三步：执行：set-ExecutionPolicy RemoteSigned
    - 第四步：选择Y，回车


# pip
* pip install [name]==      查看所有版本
* pip show [name]           查看包信息
