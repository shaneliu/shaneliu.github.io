---
layout:     post
title:      "一种留存分析的方案：Cohort Analysis"
subtitle:   " \"Cohort Analysis\""
date:       2017-06-13 12:00:00
author:     "Shane"
header-img: "img/Material-design.jpg"
tags:
    - 产品经理
    - 留存率
    - 数据分析
    - Cohort Analysis
---



前两天一篇叫[《打造 10 亿美金产品的核心秘密：用户参与层级模型》](http://t.cn/RK4kUcF)的文章在朋友圈疯转。

文章是 Pinterest 早期投资人 Sarah Tavel 总结的 __用户增长__ 模型，主要包括三个方面：

1. Growing engaged users （ 用户增长 )
2. Retaining users （ 留住用户 ）
3. Self-perpetuating （ 自我驱动 ）

<img src="/img/in-post/Cohort-Analysis/The-Hierarchy-of-Engagement.jpeg" width="100%">

<center><font color="#595959" size="1px">图片来自PPT，侵删</font></center>

对于文章中提到的这三点，我自己的理解就是做用户增长的三要素： __新增__ 、 __留存__ 、 __召回__ 。这三要素今天不展开讲了，感兴趣的朋友可以看上面的文章，今天分享一个分析留存率的方法： __Cohort Analysis__ ，这个方法很简单，也很实用，但是介绍这个方法的中文文章却不多。

---

### 什么是 Cohort Analysis ？

>Cohort analysis is a subset of behavioral analytics that takes the data from a given dataset (e.g. an eCommerce platform, web application, or online game) and rather than looking at all users as one unit, it breaks them into related groups for analysis. These related groups, or cohorts, usually share common characteristics or experiences within a defined time-span. （ 来自 wikipedia ）

解释 Cohort Analysis 之前，我们先来看一个留存曲线，如下图可见，这个产品的用户在第一个月内快速收敛，最终稳定在 10% 这个水平。

<img src="/img/in-post/Cohort-Analysis/retain.png" width="100%">

留存曲线再加上该产品的新增规模，以及单用户成本和单用户 ARPU 值，我们就能计算出这个产品的用户规模天花板，以及增长模式是不是健康。但如果我们的目标是分析该产品的留存问题，就需要用到 Cohort Analysis 了。

Cohort Analysis 可以翻译成 __群体分析__ 或 __分组分析__，其实是一种通过细分来研究数据的方法。如下表就是一个从每日新增维度细分的 Cohort Analysis 表格。

- 第一列是分组的维度，下表以用户新增的日期作为细分的维度；
- 第二列是对应的新增用户数；
- 其余列为对应分组下的用户留存率；

<img src="/img/in-post/Cohort-Analysis/cohort-analysis-table.png" width="100%">

<center><font color="#595959" size="1px">我偷懒了，图片来自网络，侵删</font></center>

---

### 怎么做 Cohort Analysis ？

Cohort Analysis 说来也简单，就是做好观察用户的分组；__分组先分维度，再分粒度。__

什么是维度？如果按用户的新增日期分组，那时间就是维度，如果按新增用户的渠道来源分组，渠道就是维度；其次是粒度，我们说的时间维度是按照月，还是按照天？这是粒度差异；新增的渠道维度，是新增的来源产品，还是来源的具体网址，这也是粒度的差异；通过基于这两方面的分组可以将对比的差异值逐级锁定，寻找原因。

对于用户的留存分析一般有两个大的分组方向：

- 从用户的获取角度分组
- 从用户的行为角度分组

##### 第一种是从用户获取的角度分组

如果按获取的时间分（ 粒度选择天或周或月，依赖于产品本身的使用频率，例如 IM 产品就适合按天看，而记事本等工具类产品就更适合按周看 ），我们就可以清晰的看到，各个时间段获取的用户在留存率表现上是不是稳定，例如上面第一个留存曲线中一个月的收敛是稳定现象，还是强烈波动平均后的结果。通过这个分析我们能圈定出流失用户做用户画像分析，并在流失率高的时间段进行干预。

同样是获取的角度，还可以通过渠道分。看不同渠道来的用户后续的留存情况。通过渠道维度的分析能够判定渠道的优劣，好的渠道可以加大投入，差的渠道可以选择淘汰。

##### 第二种是从用户行为的角度分组

从用户行为角度分组对于功能比较复杂的产品也很重要。例如现在的浏览器产品，已经不单单是解决用户访问网页的需求，还向用户提供新闻、小说、视频服务，是一个内容的综合服务体。

从用户的角度来说，选择用一个浏览器来看小说，并不是说也一定会用他来看新闻、视频。所以同样是用户流失，他可能是对不同功能模块体验的不满。

这个时候我们就可以通过用户行为这个角度分组来分析具体问题，例如在浏览器这个例子中，新闻、小说、视频都应该是每日活跃，且高留存比例的功能，如果分组中发现使用过某个功能的用户在之后的时间中留存情况很差，那就需要对这个功能做专项的优化了，相较于竞争对手有哪些方面做的不够好。

---

### 小结

Cohort Analysis 是一种简单成熟的分析方法，不但能够告诉我们用户在什么时候离开了我们的产品，而且能进一步告诉我们用户为什么离开，帮助我们找到优化产品的方法。

为了更好的使用 Cohort Analysis ，需要我们从一开始的数据打点和存储结构就做好准备。

“If you cannot measure it, you cannot improve it.” 

