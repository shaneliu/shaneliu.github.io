---
layout:     post
title:      "使用 Python 抓取百度阅读"
subtitle:   " \"创新公司:皮克斯的启示 | epub mobi 下载\""
date:       2017-05-25 12:00:00
author:     "Shane"
header-img: "img/feiwuhuanyouji.jpg"
tags:
    - Python
    - 爬虫
    - 电子书下载
    - mobi
    - epub
    - txt
    - 创新公司：皮克斯的启示
--- 

>目前只实现了下载文本内容，其中少数的几张插图被过滤掉了，争取本周内优化一个版本把插图也补上

在「百度阅读」上购买了一本《创新公司：皮克斯的启示》电子书，但坑爹的发现百度阅读 APP 的体验实在渣。于是就想看看是不是可以把电子书爬下来，放到 kindle 里面读。

<font color="595959" size = "2">
<center>一开始以为这本书就是睡前读物</center>
<center>没读一会就发现这货绝对是管理方法干货</center>
<center>尤其是对需要创造性的团队管理</center>
</font>

<img width = '100%' src = "/img/in-post/baidu-yuedu-spider/chuangxingongsi.png">

<font color="595959" size = "2">
<center>创新公司：皮克斯的启示</center>
<center> [美] 艾德·卡特姆 / 埃米·华莱士 著</center>
<center>靳婷婷 译</center>
<center>中信出版社</center>
<center>2015 年 2 月</center>
</font>

<img width = '100%' src = "/img/in-post/baidu-yuedu-spider/buy-chuangxingongsi.png">

---

接下来进入正题，如何使用 Python 爬取「百度阅读」中的内容。

### 环境准备

- Python 2.7.6：我偷懒用的是 MacBook Pro 系统自带的版本
- requests 库: 用于获取「百度阅读」返回的数据。[安装传送门](https://github.com/kennethreitz/requests)

---

### 抓取过程

整个过程大概分三个部分：

- 抓取数据
- 解析数据
- 组装存储数据

#### 1 抓取数据

一开始我想简单了，以为「百度阅读」的数据都是写在静态页面里的（如果不是低估这个事情的复杂度，我应该就不会做这个事情了）。然后__查看源码__一看傻眼了，电子书的数据是异步加载过来的。

我 Google 了好一阵技能：

在 Chrome 中用 `contrl + command + i` 打开「开发者工具」，切换到 `network` 下刷新「百度阅读」，逐一查看 `XHR` 和 `script` 两个类。

在 `script` 分类下有个 `jsonp` 请求是电子书内容，请求的地址是：

>http://wenku.baidu.com/content/49422a3769eae009581becba?m=8ed1dedb240b11bf0731336eff95093f&type=json&cn=1&_=1&t=1423309200&callback=wenku7

如果把地址里面的 `callback=wenku7` 去掉，返回的就是一个 json 字符串，这样解析起来就简单多了。

#### 2 解析数据

get 到这些信息后，就可以利用 requests 获取 json 数据，把数据打印处理研究后发现，json 的节点主要是 t 属性 和 c 属性，t 属性是用来定义 html 标签的，例如 div 、 p、 h 等等。而电子书的内容都在 c 属性内。

但 C 属性的值有两种类型，一种就是电子书内容，另一种则是另一个列表，里面又包含了 t 属性和 c 属性（嵌套关系）。

对于这种简单的嵌套关系关系使用递归函数基本就解决了。

#### 3 组装存储数据

解析完 json 的结构，直接用 `file.write()` 讲电子书的内容保存为本地的 `.txt` 文件。然后再用一个比较好用的电子书转换工具：[「calibre」](https://calibre-ebook.com/)，将`.txt` 文件转成 `.mobi` 和 `.epub` 格式。

至此整个过程就结束了，完整的代码如下（因为隐私原因隐藏了 cookie 信息）。

```python
#coding: utf8

import requests
import json

def getConnected(page):     #连接百度阅读，获取 json 数据
    url ='https://wenku.baidu.com/content/ebookID'
    header = {
    'User-Agent' : 'Mozilla/5.0 ……',
    'Cookie' : baiduID
    }
    data = {
    'm': ebookToken,
    'type': 'json',
    'cn': page,  #一共17页
    }

    r = requests.get(url, headers = header, params = data)
    parseDom(r.json())

def parseDom(json_dict):        #解析 json 树，获取电子书内容
    ebook = open('~/chuangxingongsi.txt', 'a')
    if isinstance(json_dict, dict):
        for item in json_dict:
            if item == 't':
                print 'tag is : %s' % json_dict[item]
            elif item == 'style':
                print 'style is : %s' % json_dict[item]
            elif item == 'blockNum':
                print 'blockNum is : %s' % json_dict[item]

            ……    #为了减少篇幅，删除了部分标签，完全不影响文本内容的抓取

            elif item == 'c':
                if isinstance(json_dict[item], list):
                    for sub_item in json_dict[item]:
                        parseDom(sub_item)
                else:
                    print 'content is : '
                    print json_dict[item].encode('utf8')
                    ebook.write(json_dict[item].encode('utf8'))
            else:
                print json_dict.keys()
    else:
        print 'something is wrong!'
    ebook.close()

def crawlContent():
    for page in xrange(1,18):
        getConnected(page)

if __name__ == '__main__':
    crawlContent()

```

---

### 小结

- 代码基本是以实用主义出发了，是能用就行，后面遇到实用过程中问题再继续优化。
- 惯例：需要《创新公司》电子书，可以到公号：「勰门歪道」回复 **创新公司** 获取；





