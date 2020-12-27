## Python3 环境配置（CentOS)
### 下载，编译，安装
1. 安装必要依赖：yum install -y openssl-devel bzip2-devel expat-devel gdbm-devel readline-devel sqlite-devel
2. 下载：wget https://www.python.org/ftp/python/3.6.5/Python-3.6.5.tgz
3. 解压：tar -xzvf Python-3.6.5.tgz
4. 进入解码目录：cd Python-3.6.5
5. 安装GCC： yum install -y gcc
6. 创建编译目录： mkdir /usr/local/python
7. 编译Python3：./configure --prefix=/usr/local/python
8. 安装：make
        make install

### 设置Python3 替换 python2
1. 修改软连接: ln -s /usr/local/python/bin/python3.6 /usr/bin/python
                ln -s /usr/local/python/bin/pip3.6 /usr/bin/pip
2. 安装 setuptools
    * wget --no-check-certificate https://pypi.python.org/packages/source/s/setuptools/setuptools-19.6.tar.gz#md5=c607dd118eae682c44ed146367a17e26 
    * 解压：tar -zxvf setuptools-19.6.tar.gz 
    * 进入：cd setuptools-19.6
    * 编译：sudo python3 setup.py build 
    * 按章：sudo python3 setup.py install
3. 安装 pip3
    * wget --no-check-certificate https://pypi.python.org/packages/source/p/pip/pip-8.0.2.tar.gz#md5=3a73c4188f8dbad6a1e6f6d44d117eeb 
    * tar -zxvf pip-8.0.2.tar.gz 
    * cd pip-8.0.2 
    * sudo python3 setup.py build 
    * sudo python3 setup.py install
    * sudo ln -s /usr/local/python3/bin/pip3 /usr/bin/pip
    * pip install --upgrade pip


### shadowsocks
pip install shadowsocks
后台启动：sudo ssserver -p 443 -k password -m rc4-md5 --user nobody -d start
停止：sudo ssserver -d stop
查看日志：sudo less /var /log/shadowsocks.log

    