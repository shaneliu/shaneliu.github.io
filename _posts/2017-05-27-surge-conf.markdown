---
layout:     post
title:      "Surge for Mac 初体验与教程"
subtitle:   " \"科学上网之路\""
date:       2017-05-27 12:00:00
author:     "iamshane"
header-img: "img/surge-4-mac.jpg"
tags:
    - Mac
    - Surge
    - 科学上网
    - 工具
    - 教程
    - ShadowsocksX-NG
    - 配置
    - manual
--- 



>本文主体转载自 [CloudStone](http://cloudstone.xin/2016/10/31/Mac-Surge-2-%E5%88%9D%E4%BD%93%E9%AA%8C/) 的博文，根据我自己的情况做了少量修改


在iPhone 上使用 Surge 科学上网已经一段时间了，这两天在朋友的鼓动下，终于打算入坑使用Surge for Mac 。

买了 License 之后，在家一顿折腾，Google了一晚上，找到的文章，大部分讲的是Surge for iOS或者Surge for mac 1.x，我看的莫名其妙。其中几篇提供了配置文件模板，但大都讲的不清不楚。

终于找到这篇文章，简单的把配置讲清楚了。

---

接下来进入正题，官方称Surge是一款网络调试工具，而大部分人用它当传送门，两者都没错。

- 传送门：一方面很多专业上的搜索还是习惯依赖 Google ，另一方面作为PM，经常需要更广阔的资源，看看别人家最近火热的产品到底什么样子。
- 网络调试工具：作为移动端开发者，抓包调接口是家常便饭，而对于移动web开发者则更加有意义。因为我们可以通过设置客户端代理，将静态资源代理到本地，调试线上应用，内个feel倍儿爽~如果是调试单页应用，就更省心了。

接下来，我们一个个搞定。

---

### 传送门

这个算是刚需，也是我使用 Surge 的主要原因。

1. 打开 Surge
2. 首次打开，Surge 会在文稿目录下创建带有示例配置的Surge目录。
3. 点开状态栏上的Surge菜单，选择『Set as System Proxy』,顾名思义Surge成为系统代理，几乎所有 http(s) 请求都会被拦截，但 shell 的网络请求并不会被拦截（下文再说如何让 shell 也出墙）
4. 翻山越岭最终选择了 [AbcLite](http://www.abclite.cn/1995.html) 的这个配置作为基础。
复制其内容并保存到 `~/Documents/Surge` 目录下，比如 `my-surge.conf` 。

重点来了,请看：

```
[Proxy]
   🇭🇰 HK = custom,${ss-server host},${ss-server port},${ss encrypt type},${ss-password},https://github.com/stoneChen/Surge-config/raw/master/SSEncrypt.module
   🇸🇬 SG = custom,${ss-server host},${ss-server port},${ss encrypt type},${ss-password},https://github.com/stoneChen/Surge-config/raw/master/SSEncrypt.module
   🇯🇵 JP = custom,${ss-server host},${ss-server port},${ss encrypt type},${ss-password},https://github.com/stoneChen/Surge-config/raw/master/SSEncrypt.module
   🇺🇸 US = custom,${ss-server host},${ss-server port},${ss encrypt type},${ss-password},https://github.com/stoneChen/Surge-config/raw/master/SSEncrypt.module
   🇰🇷 KR = custom,${ss-server host},${ss-server port},${ss encrypt type},${ss-password},https://github.com/stoneChen/Surge-config/raw/master/SSEncrypt.module
   
[Proxy Group]
    Proxy = select,🇭🇰 HK,🇸🇬 SG,🇯🇵 JP,🇺🇸 US,🇰🇷 KR
```

`[Proxy]` 是具体的代理配置，它下面就是5个 ss 服务器节点, 这里只是5个国家例子，根据你拥有的ss账号数来决定，拥有几个账号就留下其中几个对应国旗配置就好。表面上看就是5个键值对(键可以自定义)，键中加上国旗可以很直观的区分不同国家的 ss 节点，值中的变量分别表示：

- ss-server host: ss主机，ip或域名
- ss-server port: ss主机端口
- ss encrypt type: 加密方式
- ss-password: ss密码

`custom`不能改，是一个约定类型(ss协议)，最末一项是ss模块下载地址，也不需要改,当选择了当前配置所在的配置文件，Surge会去下载ss模块，有弹窗提示。

`[Proxy Group]` 是一个组策略配置，它的某一项配置可以引用 `[Proxy]` 中的配置，也可以引用其他的组策略配置。这里有 `select` ,  `url-test` ,  `ssid` 三种策略可以用，具体请阅读 `example-chinese.conf` 中的注释。

简单讲：

- select：在菜单上手动选择ss节点
- url-test：定时轮询向指定的地址发起请求，哪个节点响应时间最短，则切换到哪个ss节点
- ssid： 根据wifi名字进行切换ss节点

ss 配置完毕后，保存。然后点击状态栏中的 Surge ,选择 `Switch Configuration` , 右侧会出现 `~/Documents/Surge` 下的配置文件列表，选择刚刚的 `my-surge.conf`。

上个图：

<img width="100%" src="/img/in-post/surge-conf/surge.conf.jpeg" />

__然后就是见证奇迹的时刻~__

打开浏览器: `http://www.google.cn/` 肥车~

外面的世界很精彩~

---

### 网络规则设置

有5种匹配规则：

- DOMAIN: 基于域名
- DOMAIN-SUFFIX: 基于域名后缀
- DOMAIN-KEYWORD: 基于域名关键字
- IP-CIDR: 基于”无类别域间路由”，具体我也不懂啥意思，大概就是基于IP段
- GEOIP: 表示IP所属区域，有CN(中国),US(美国)等值

匹配规则后，可以对匹配的请求作出三种处理

- DIRECT
- REJECT
- ${某个自定义策略}

__举个栗子：__

- DOMAIN-SUFFIX, *.google.com,Proxy # 所有以google.com结尾的请求，都走Proxy代理
- DOMAIN,xyz.cn,DIRECT # xyz.cn的请求，都走直连
- DOMAIN-KEYWORD, advertise,REJECT # 所有域名中带advertise的请求，都拒绝
- IP-CIDR,61.160.200.252/32,REJECT # 屏蔽61.160.200.252这个ip
- GEOIP,CN,DIRECT # 国内IP都走直连

---

### 广告屏蔽

这个是Surge的特色之一，只要匹配规则，就可以直接拒绝网络请求，从而阻止广告。

基于上面的例子，我们继续扩展：

```
DOMAIN-KEYWORD, advertise,REJECT
DOMAIN-SUFFIX,stat.tudou.com,REJECT
DOMAIN-SUFFIX,stat.youku.com,REJECT      
DOMAIN-SUFFIX,strip.taobaocdn.com,REJECT
```

看懂了么？偷偷告诉你，视频广告也可以屏蔽奥~(亲测 youku ，tudou 有效)

如果在以后的上网过程中，你遇到了『漏网』的广告，打开你的 Surge 配置文件，添加相应的配置，就可以干掉它了，世界就变得清静多了。

---

### 让shell也能出墙

默认情况下， shell 不会被代理，我们需要设置 shell 环境变量，将代理服务指向 Surge 的端口。

将以下代码复制到 `~/.zshrc` 的底部

```
proxy=http://127.0.0.1:6152
export http_proxy=$proxy
export https_proxy=$proxy
export ftp_proxy=$proxy
```

---

###代理转发网络请求

这个功能，基于URL Rewrite配置实现，简单讲，就是写正则。举个栗子：

```
[URL Rewrite]
^http://a.net/m/(.*) http://b.net:9999/m/$1
```

意思就是，所有以 `http://a.net/m/` 开头的 url 全部代理到 `http://b.net:9999/m/` 下(注意中间的空格)。

用代码解释就是：

```
let regStr = new RegExp('^http://a.net/m/(.*)')
let proxyUrl = url.replace(regStr, 'http://b.net:9999/m/$1')
```

当有请求匹配该规则，就会被代理转发，在 Surge Dashboard 上会看到代理后的记录.

规则可以设置多条。

这样写，默认是 `header` 模式，客户端不会感知到当前请求被代理了。上面配置的等价写法是：

```
^http://a.net/m/(.*) http://b.net:9999/m/$1 header
```

还有一种模式是302重定向，客户端是可感知的,302模式这样写：

```
^http://aaa.com http://bbb.cn 302
```

这样 `http://aaa.com` 就被重定向到 `http://bbb.cn` 了。

如此一来，只要你正则玩的溜，各种代理转发随你翻转~

有时候，通过域名规则过滤广告太暴力，有时候只是想屏蔽指定域名下个别请求，那么 `URL Rewrite` 就能实现，针对不想看到的东西，撸一个正则，转发到不可响应的地址即可(比如 loclahost )。

---

### Host设置

这个配置不仅包含了本机的 `/etc/hosts` 功能，而且还提供了 泛解析 和 别名 支持，相当好用。

举个栗子：

```
[Host]
# 这个是泛解析,a.test.com  b.test.com 等通通指向 192.168.1.100
*.test.com = 192.168.1.100
# 这个是别名设置，c.me  d.me 等通通指向localhost
*.me = localhost
```

---

### 小结

Surge无疑是很强大的，称之为『神器』不为过，其价格导致很多人望而却步。所以这里推荐另外一款科学上网的工具：[ShadowsocksX-NG](https://github.com/shadowsocks/ShadowsocksX-NG)


