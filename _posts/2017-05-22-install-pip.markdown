---
layout:     post
title:      "mac安装pip工具"
subtitle:   " \"使用brew报错的解决方案\""
date:       2017-05-22 12:00:00
author:     "iamshane"
header-img: "img/install-pip.jpg"
tags:
    - Mac
    - Python
---


>pip 是 python 常用的包管理器， Mac 自带 python ，但是没有自带 pip 工具，使用 brew 安装 pip 时报错如下：

```
➜  ~brew install pip

Error: No available formula with the name "pip"
Homebrew provides pip via: `brew install python`. However you will then
have two Pythons installed on your Mac, so alternatively you can install
pip via the instructions at:

	https://pip.readthedocs.org/en/stable/installing/#install-pip
```

提示需要使用brew安装python，然后会连pip一起安装，目前系统自带的python是2.7.10，已经够我使用了，不准备再安装别的版本的python，否则还要进行版本切换，所以换种方式安装pip，安装如下：

```
$ sudo easy_install pip
```

安装成功！

__备注：__

安装成功后运行`pip list`可能有一下告警：

```
➜  ~ pip list

DEPRECATION: The default format will switch to columns in the future. You can use --format=(legacy|columns) (or define a format=(legacy|columns) in your pip.conf under the [list] section) to disable this warning.
```

在`~/.pip/pip.conf`文件末尾添加`format=columns`即可。



