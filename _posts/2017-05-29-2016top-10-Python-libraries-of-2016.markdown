---
layout:     post
title:      "Top 10 Python libraries of 2016"
subtitle:   " \"from tryo labs\""
date:       2017-05-29 12:00:00
author:     "tryo labs"
header-img: "img/python.png"
tags:
    - Python
    - 学习笔记
--- 


>本文转载自[tryo labs](https://tryolabs.com/blog/2016/12/20/top-10-python-libraries-of-2016/)

Last year, we did a recap with what we thought were [the best Python libraries of 2015](https://tryolabs.com/blog/2015/12/15/top-10-python-libraries-of-2015/), which was widely shared within the Python community (see post in [r/Python](https://www.reddit.com/r/Python/comments/3wyiuv/top_10_python_libraries_of_2015/)). A year has gone by, and again it is time to give due credit for the awesome work that has been done by the **open source community** this year.

Again, we try to avoid most established choices such as Django, Flask, etc. that are kind of standard nowadays. Also, some of these libraries date prior to 2016, but either they had an explosion in popularity this year or we think they are great enough to deserve the spot. Here we go!

---

### 1. [Zappa](https://www.zappa.io/)

Since the release of AWS Lambda (and others that havefollowed), all the rage has been about serverless architectures. These allow microservices to be deployed in the cloud, in a fully managed environment where one doesn’t have to care about managing any server, but is assigned stateless, ephemeral computing containersthat are fully managed by a provider. With this paradigm, events (such as a traffic spike) can trigger the execution of more of these containers and therefore give the possibility to handle “infinite” horizontal scaling.

Zappa is **the serverless framework for Python**, although (at least for the moment) it only has support for AWS Lambda and AWS API Gateway. It makes building so-architectured apps very simple, freeing you from most of the tedious setup you would have to do through the AWS Console or API, and has all sort of commands to ease deployment and managing different environments.

---

### 2. [Sanic](https://github.com/channelcat/sanic) + [uvloop](https://magic.io/blog/uvloop-blazing-fast-python-networking/)

Who said Python couldn’t be fast? Apart from competing for the best name of a software library ever, Sanic also competes for the fastest Python web framework ever, and appears to be the winner by a clear margin. It is a Flask-like Python 3.5+ web server that is designed for speed. Another library, uvloop, is an ultra fast drop-in replacement for asyncio’s event loop that uses libuv under the hood. Together, these two things make a great combination!

According to the Sanic author’s benchmark, uvloop could power this beast to handle more than **33k requests/s** which is just insane (and faster than node.js). Your code can benefit from the new async/await syntax so it will look neat too; besides we love the Flask-style API. Make sure to give Sanic a try, and if you are using asyncio, you can surely benefit from uvloop with very little change in your code!

---

### 3. [asyncpg](https://github.com/MagicStack/asyncpg)

In line with recent developments for the asyncio framework, the folks from [MagicStack](https://magic.io/) bring us this efficient asynchronous (currently CPython 3.5 only) database interface library designed specifically for PostgreSQL. It has zero dependencies, meaning there is no need to have libpq installed. In contrast with psycopg2 (the most popular PostgreSQL adapter for Python) which exchanges data with the database server in text format, asyncpg implements PostgreSQL **binary I/O protocol**, which not only allows support for generic types but also comes with numerous performance benefits.

The benchmarks are clear: asyncpg is on average, at least **3x faster** than psycopg2(or aiopg), and faster than the node.js and Go implementations.

---

### 4. [boto3](https://github.com/boto/boto3)

If you have your infrastructure on AWS or otherwise make use of their services (such as S3), you should be very happy that boto, the Python interface for AWS API, got a completely rewrite from the ground up. The great thing is that you don’t need to migrate your app all at once: you can use boto3 and boto (2) at the same time; for example using boto3 only for new parts of your application.

The new implementation is much **more consistent** between different services, and since it uses a data-driven approach to generate classes at runtime from JSON description files, it will always get fast updates. No more lagging behind new Amazon API features, move to boto3!

---

### 5. [TensorFlow](https://www.tensorflow.org/)

Do we even need an introduction here? Since it was released by Google in November 2015, this library has gained a huge momentum and has become the #1 trendiest GitHub Python repository. In case you have been living under a rock for the past year, TensorFlow is a library for **numerical computation** using data flow graphs, which can run over GPU or CPU.

We have quickly witnessed it become a trend in the Machine Learning community (especially Deep Learning, see our post on [10 main takeaways from MLconf](https://tryolabs.com/blog/2016/11/18/10-main-takeaways-from-mlconf/)), not only growing its uses in research but also being widely used in production applications. If you are doing Deep Learning and want to use it through a higher level interface, you can try using it as a backend for Keras (which made it to last years post) or the newer TensorFlow-Slim.

---

### 6. [gym](https://gym.openai.com/) + [universe](https://universe.openai.com/)

If you are into AI, you surely have heard about the OpenAI non-profit artificial intelligence research company (backed by Elon Musk et al.). The researchers have open sourced some Python code this year! Gym is a toolkit for developing and comparing reinforcement learning algorithms. It consists of an open-source library with a collection of test problems (environments) that can be used to test reinforcement learning algorithms, and a site and API that allows to compare the performance of trained algorithms (agents). Since it doesn’t care about the implementation of the agent, you can build them with the computation library of your choice: bare numpy, TensorFlow, Theano, etc.

We also have the recently released universe, a software platform for researching into general intelligence across games, websites and other applications. This fits perfectly with gym, since it allows any real-world application to be turned into a gymenvironment. Researchers hope that this limitless possibility will **accelerate research** into smarter agents that can solve general purpose tasks.

---

### 7. [Bokeh](http://bokeh.pydata.org/en/latest/)

You may be familiar with some of the libraries Python has to offer for data visualization; the most popular of which are matplotlib and seaborn. Bokeh, however, is created for **interactive visualization**, and targets modern web browsers for the presentation. This means Bokeh can create a plot which lets you explore the data from a web browser. The great thing is that it integrates tightly with Jupyter Notebooks, so you can use it with your probably go-to tool for your research. There is also an optional server component, bokeh-server, with many powerful capabilities like server-side downsampling of large dataset (no more slow network tranfers/browser!), streaming data, transformations, etc.

Make sure to check the gallery for examples of what you can create. They look awesome!

---

### 8. [Blaze](https://blaze.readthedocs.io/en/latest/index.html)

Sometimes, you want to run **analytics** over a dataset too big to fit your computer’s RAM. If you cannot rely on numpy or Pandas, you usually turn to other tools like PostgreSQL, MongoDB, Hadoop, Spark, or many others. Depending on the use case, one or more of these tools can make sense, each with their own strengths and weaknesses. The problem? There is a big overhead here because you need to learn how each of these systems work and how to insert data in the proper form.

Blaze provides a **uniform interface** that abstracts you away from several database technologies. At the core, the library provides a way to express computations. Blaze itself doesn’t actually do any computation: it just knows how to instruct a specific backend who will be in charge of performing it. There is so much more to Blaze (thus the ecosystem), as libraries that have come out of its development. For example, Dask implements a drop-in replacement for NumPy array that can handle content larger than memory and leverage multiple cores, and also comes with dynamic task scheduling. Interesting stuff.

---

### 9. [arrow](https://github.com/crsmithdev/arrow)

There is a famous saying that there are only two hard problems in Computer Science: cache invalidation and naming things. I think the saying is clearly missing one thing: **managing datetimes**. If you have ever tried to do that in Python, you will know that the standard library has a gazillion modules and types: datetime, date, calendar, tzinfo, timedelta, relativedelta, pytz, etc. Worse, it is timezone naive by default.

Arrow is “datetime for humans”, offering a sensible approach to creating, manipulating, formatting and converting dates, times, and timestamps. It is a replacement for the datetime type that supports Python 2 or 3, and provides a much nicer interface as well as filling the gaps with new functionality (such as humanize). Even if you don’t really need arrow, using it can greatly reduce the boilerplate in your code.

---

### 10. [hug](http://www.hug.rest/)

Expose your internal API externally, drastically simplifying Python APIdevelopment. Hug is a next-generation Python 3 (only) library that will provide you with the cleanest way to create HTTP REST APIs in Python. It is not a web framework per se (although that is a function it performs exceptionally well), but only focuses on exposing idiomatically correct and standard internal Python APIs externally. The idea is simple: you define logic and structure once, and you can expose your API through multiple means. Currently, it supports exposing REST API or command line interface.

You can use type annotations that let hug not only generate documentation for your API but also provide with validation and clean error messages that will make your life (and your API user’s) a lot easier. Hug is built on Falcon’s high performance HTTP library, which means you can deploy this to production using any wsgi-compatible server such as gunicorn.

At Tryolabs we excel at developing heavy Python backends with Machine Learning components. If you need some help in these kind of projects, drop us a line to hello@tryolabs.com (or fill out this form) and we’ll happily connect.
