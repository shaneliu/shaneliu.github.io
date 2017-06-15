---
layout:     post
title:      "Sublime Text 3 Mac 指南"
subtitle:   " \"最好的编辑器\""
date:       2017-05-28 12:00:00
author:     "Shane"
header-img: "img/writing.jpg"
tags:
    - Mac
    - Sublime Text 3
    - Sublime Text
    - PC
    - 效率工具
    - manual
--- 

>本文转自 [kpman \| code](https://code.kpman.cc/2014/10/14/sublime-text-3-mac-%E6%8C%87%E5%8D%97/) 的博客，作为查询快捷键的备忘

本篇是我根据自己使用习惯所做的快捷键整理，使用sublime text这套编辑器已经有2年之余，本身是个快捷键爱好者，对于发掘好用的快捷键乐此不疲，因此整理常用的快捷键在这篇，针对的是mac使用者所使用者快捷键，希望对各位有帮助。

---

### 快捷键

左边是本篇所采用的缩写，右則是键盘上面的标示：

- cmd = command
- shift = shift
- option = option (alt)
- control = control
- pkg-ctrl = package control (command + shift + p)

---


### 基础模式

「基础模式」介绍非 sublime 专用的快捷键，是一般使用者都可以快速上手的部分，想要看进阶的可以跳过这部份。

#### 1. cmd + o (open)

快速开启整个资料夹(专案)

#### 2. cmd + w

关闭视窗分页

#### 3. cmd + n

开新分页

#### 4. cmd + shift + t

重新开启刚刚关闭的分页

#### 5. cmd + shift + v

贴上时，符合缩排

---

### 画面配置

以下介绍 sublime 的画面配置，常常因为编辑情境的所需，利用快捷键让自己的画面配置更加有弹性。

#### 1. cmd + option + 数字

分割视窗，让你的编辑范围有多个 panel 。

常用为 cmd + option + 1 和 cmd + option + 2 之间切换。

使用情境：左边 `.html`右边 `.css` ，编辑起来快速又方便。

建议：利用空白键右边的两个连续按钮搭配数字。

<img width = '100%' src='/img/in-post/sublime-text-3-mac/no1.gif'>

#### 2. cmd + k 再 cmd + b

关闭左侧资料夹目录，让画面变得更宽敞。

这是我非常使用的一个快捷键，可以让编辑的区域变得更大。

<img width = '100%' src='/img/in-post/sublime-text-3-mac/no2.gif'>

#### 3. cmd + shift + control + f

进入 zen 状态，单份文件变成全萤幕，且左边会自动缩排。

使用情境：当不常需要切换档案时，此模式可以专注在单一档案上，打这篇 blog 时我便这样使用。

建议：快捷键不好记，可以点选 `View --> Enter Distraction Free Mode`


<img width = '100%' src='/img/in-post/sublime-text-3-mac/no3.png'>

---

### 选取

底下介绍的部份，回到 sublime text 编辑器本身，因为重点在编辑部分，因此在此将「选取」特别整理成一区。

#### 1. cmd + d (可连按)

快速选取一范围内的字串，连按d的话会选取整份文件内相同的字串。

当选取完后，可以直接打字，因此就可以将整份文件的字串全部改成新字串。

<img src='/img/in-post/sublime-text-3-mac/no4.gif'>

#### 2. cmd + l (可连按)

选取游标在内的一行，连按 l 的话会往下选取下面的行数。

#### 3. cmd + shift + l

此功能常与上述 `cmd + l` 配合，当选取多行后，按下 `cmd + shift + l` ，则会在多行的情况结尾出现游标，可以做多行编辑。

<img src='/img/in-post/sublime-text-3-mac/no5.gif'>

#### 4. option + 滑鼠拖拉

当按住 option 后，搭配滑鼠拖拉便可以一次选取多行，并且产生游标。
注意：拖曳的时候，滑鼠必须是由上到下垂直的选取状态

<img src='/img/in-post/sublime-text-3-mac/no6.gif'>

#### 5. cmd + 滑鼠点选

按住cmd后，利用滑鼠在文件内点选，便可以在任何位置新增游标，产生多选状态做编辑。

<img src='/img/in-post/sublime-text-3-mac/no7.gif'>

#### 6. cmd + 左 或 右

让你的游标可以快速的回到该行的最前面或是最后面。

<img src='/img/in-post/sublime-text-3-mac/no8.gif'>

#### 7. shift + 左 或 右

每按一次会选择一个字元，可以更加精准的选取自己要的部份。

<img src='/img/in-post/sublime-text-3-mac/no9.gif'>

8. cmd + shift + 左 或 右

从游标所在处，往前选取或者往后选取该行到底。

<img src='/img/in-post/sublime-text-3-mac/no10.gif'>

---

### 查找

在sublime里面寻找的功能做的非常强大，不论是文件内、或是文件名称都可以快速找到。
底下将会利用 `GoTo Anything` 这个强大的内建功能来实作。

#### 1. cmd + p + 输入档名

利用 `cmd + p` ，之后等视窗出现后，即可输入你要找的档名，按下 `enter` 即可开启。

<img src='/img/in-post/sublime-text-3-mac/no11.gif'>

#### 2. cmd + p + “:” + 行数

此功能相同于 `control + g` ，可以快速的跳到你指定的行数。

<img src='/img/in-post/sublime-text-3-mac/no12.gif'>

#### 3. cmd + p + “@” + function name

此功能相同于 `cmd + r` ，可以快速跳到定义的 function 

建议：若是知道要找 function ，建议使用这个而非使用 `cmd + f`

<img src='/img/in-post/sublime-text-3-mac/no13.gif'>

#### 4. cmd + p + “#” + keyword

此功能可以快速找到文件内的关键字。

个人比较少用这个功能，利用 `cmd + f` 时，可以持续按 `enter` 找到目标。

#### 5. cmd + shift + f

全文搜寻，可以找出「整个project」内的关键字。

在 Find Result 内，点选两下，便可以跳到该文件，这是我觉得最实用的部份。

<img src='/img/in-post/sublime-text-3-mac/no14.gif'>

---

### 快还要更快

#### 1. cmd + control + 上 或 下

将选取起来的行，整段往上或往下移动。

使用情境：当几行code需要移动不算太大范围的时候，可以使用这个快捷键，而不用剪下再贴上。

<img src='/img/in-post/sublime-text-3-mac/no15.gif'>

#### 2. cmd + /

将该行注解。
个人建议：搭配 `cmd + l(连按)` 可以选取多行，一次注解起来。

<img src='/img/in-post/sublime-text-3-mac/no16.gif'>

---

### reference

1. [GETTING STARTED WITH SUBLIME TEXT 3: 25 TIPS, TRICKS, AND SHORTCUTS](https://generalassemb.ly/blog/sublime-text-3-tips-tricks-shortcuts/)
2. [Sublime Text 全程指南](http://zh.lucida.me/blog/sublime-text-complete-guide/)

















































