
# vscode 

## lanucher.json 配置
- "pargram": "${workspaceFolder}\\main.py"      固定文件启动
- "args": ['arg1', 'arg2']                      启动参数
- "justmycode": false                           调试源码

## err
* venv/Scripts/activate 无法执行
    - 第一步：以管理员身份运行powershell
    - 第二步：执行：get-ExecutionPolicy 回复Restricted，表示状态是禁止的。
    - 第三步：执行：set-ExecutionPolicy RemoteSigned
    - 第四步：选择Y，回车

