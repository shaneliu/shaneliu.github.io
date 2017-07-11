---
layout:     post
title:      "Ubuntu 下安裝 Oh-my-zsh"
subtitle:   " \"How to install Oh-my-zsh on Ubuntu\""
date:       2017-06-14 12:00:00
author:     "Shane"
header-img: "img/coding.jpg"
tags:
    - Ubuntu
    - 阿里云
    - Zsh
    - Oh-my-zsh
---


心血来潮买了阿里云的服务器开着倒腾，服务器默认的 Shell 是 Bash ，第一想法就是换成自己趁手的 Shell ： Oh-my-zsh ，着手开始安装。

---

### 安裝 Oh-my-zsh

安装 Oh-my-zsh 之前需要先安裝 Zsh 套件

```
$ apt-get install zsh
```

我在安装 Zsh 的时候遇到了一些小问题，返回 `Unable to locate package` 错误，网上找了一大堆解决方案，最后很简单。

先升级一下 `apt-get` ，然后再安装 Zsh 就成功了。

```
$ apt-get update
```

安装git

```
$ apt-get install git
```

安装完以上两步，执行下面的代码

```
curl -L https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh | sh
```

把zsh设置成默认-替换bash

```
chsh -s /bin/zsh
```

---

### 配置 Oh-my-zsh

安装 Oh-my-zsh 不就是为了主题和插件么，2333……

主题修改，我喜欢 `ys` 这款主题，官方也提供了[各种主题](https://github.com/robbyrussell/oh-my-zsh/wiki/External-themes)，大家可以取需。

打开配置文件

```
$ vim ~/.zshrc 
```

配置文件里找到：（输入`/`即可搜素ZSH_THEME） `ZSH_THEME="robbyrussell"` 修改为： `ZSH_THEME="ys"`

然后 `：wq` 保存退出就完成了。

### 常用命令

查看zsh下有哪些主题

```
$ ls ~/.oh-my-zsh/themes
```


查看zsh下有哪些插件

```
ls ~/.oh-my-zsh/plugins
```

<img src="/img/in-post/install-zsh/ys-zsh-theme.jpg" width="100%">
