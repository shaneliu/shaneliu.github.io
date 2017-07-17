---
layout:     post
title:      "阿里云上部署 Flask 最小的应用"
subtitle:   " \"How to deploy Flask on the Aliyun ？\""
date:       2017-06-16 12:00:00
author:     "Shane"
header-img: "img/coding.jpg"
tags:
    - 阿里云
    - Python
    - Flask
---


我之前整了一些 `Python` 的脚本，想着用 Flask 弄一个最简单的 web 服务放到阿里云上去，目标是能在公网访问就行。

因为太小白最后花了很多时间，网上很多教程步子都比较大，一弄就是整一堆的框架 `WSGI` 、 `Nginx`  ，这里记录一个最最小白的版本：只用 `Flask` 。

---

### 系统环境

首先得注册账号买一个 __云服务器__ ，我的配置：

- 系统环境：Ubuntu 16.04 64位
- CPU：1 核
- 内存：2 GB

通过 `SSH` 连接服务器

```zsh
ssh root@你的云服务器地址
```

第一次连接服务器，终端会询问是否保存密钥，一般键入：Y 即可。之后输入root账号对应的密码，终端提示：

>Welcome to aliyun Elastic Compute Service!

表示连接服务器成功，就可以开始在阿里云上部署最简单的环境了。 

### 安装 pip

后续工具的安装需要 `pip` 工具的支持，先安装 `pip` ：

```zsh
sudo apt-get install python-pip
```

与前面一样，遇到询问确认时，键入 Y 回车，看到 `Setting up python-pip` 就是装好了。

### 安装 virtualenv

`virtualenv`  是用来为一个应用创建一套“隔离”的 `Python` 运行环境，装不装其实都不影响最后 `Flask` 的部署。

我主要是考虑到摸索期经常经常要装很多第三方的包，所以在 `virtualenv` 实验，出问题的时候恢复起来方便一些。

##### 首先，用 pip 安装 virtualenv

```zsh
$ pip install virtualenv
```

然后，需要一套独立的 `Python` 运行环境，可以这么做：

##### 第一步，创建目录

```zsh
$ mkdir myproject
$ cd myproject/
```

##### 第二步，创建一个独立的Python运行环境，命名为venv

```zsh
$ virtualenv venv
```

新建的Python环境被放到当前目录下的venv目录。有了venv这个Python环境，可以用source进入该环境：

```zsh
$ source venv/bin/activate
(venv)Mac:myproject michael$
```

注意到命令提示符变了，有个 `(venv)` 前缀，表示当前环境是一个名为 `venv` 的 `Python` 环境。

>注释： 退出当前的 `venv` 环境，使用 `deactivate` 命令

### 安装 Flask

```
$ pip install flask
```

### 最小的应用

写一个最简单的应用 `hello.py`

```python
# coding=utf-8

__author__ = 'shane lshane1985@gmail.com'
__create_time__ = '17/7/12'

from flask import Flask
import sys

reload(sys)
sys.setdefaultencoding('utf-8')

app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello World!'

if __name__ == '__main__':
    app.run(host='0.0.0.0',port='80')
```

阿里云默认只开放了 22 端口，所以需要到 __安全组__ 配置一下，增加对 80 端口的支持。

### 使用 SPTF 上传代码

我使用 Sublime Text 的 SPTF 插件做代码同步，插件的安装和配置网上教程很多，这楼不赘述，[传送门](http://www.jianshu.com/p/8e557deee70a)。

强调一下，我在配置服务器路径的时候遇到了一些小问题，如果路径是建在 `root` 账号之下，记得在路径中加上 `/root/` ，例如我需要把 `hello.py` 放到 `home/shane/my-project` 下，配置的时候就填 `/root/home/shane/my-project/`

### 启动服务

完成上述步骤之后，就可以在阿里云启动 `hello.py` 服务了：

```
$ cd home/shane/my-project
$ python hello.py
```

### 访问服务

自此一个最简单的 `Flask` 服务就已经完成了，通过 __阿里云服务器的IP__ 直接可以在浏览器中访问服务。








