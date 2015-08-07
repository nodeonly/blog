---
layout: post
title: "mongoose-cli"
description: ""
keywords: ""
category: 
tags: []
---

一直以来mongoose学习都是比较麻烦的，mongoose-cli试图简化学习和测试mongoose部分，并通过app开发流程反思整个过程中业务逻辑部分如何抽象，以期简化开发与分层实现

## app开发流程

如图

![](/css/2015-08-07/1.png)

这里首先从交互图开始，需求统一为交互图。

- 开发拿到交互图，首先要根据交互【拆分功能点】
- 根据功能点形成【api文档】
- 根据功能点和已有model进行【建模】
- 根据模型，【模拟数据】，并校验模型直到可行
- 根据功能点+模型，编写api接口

那么，我们看看这个流程里什么是最核心的东西？

- 功能点
- 模型

这2点其实是整个app里最核心的部分，即业务部分，我们如果把握住此处的设计，输出【api文档】 + 模型，即可拆分工作任务，WBS

## 业务建模

- 避免过度设计，够用就好
- 如果时间允许就给以后多留点扩展

## nodejs + mongodb（mongoose）

根据上面的流程，结合MEAN架构，需要交付

- api文档
- mongoose模型

### 如何简化api文档？

能够根据api文档生成routes和controller部分代码，并且可逆

留空model和service即可。


### 如何简化model操作？

- scaffold 脚手架，可以快速完成模型相关crud操作，界面也可以。
- moa-console 控制台，在命令行即可测试模型方法等
- mongoose-cli 随时随地，测试model，融合bluebird等promise库，让业务处理更简单
- 可以把model直接打包发布到npm (TODO)

### 模型固化成node module的意义

- 复用，多系统共享model
- 可以通过xxx@1.0类似的版本，在npm里进行版本限定
- 耦合低
- 测试容易
- 新人培训容易


## mongoose-cli

上面是对于业务建模的思考，那么我们如何快速的进行建模，又能不和现有代码耦合呢？

之前说过，业务逻辑，基本就是model + 流程控制，能否直接都集成到一起？

mongoose-cli主要解决的就是这个问题

### mongoose best practice

- mongoose + mongoosedao
- bluebird

### Install 

```
[sudo] npm install -g mongoose-cli
```


### Usage


第一步：使用`mongoose`命令来初始化测试目录结构


```
➜  d  mongoose
➜  d  cd mongoose-console 
➜  mongoose-console  ls
LICENSE      README.md    app          config       db.js        example.js   index.js     node_modules package.json
                                                                                
                                                                                                                                         ➜  mongoose-console  mc
```


第二步： 执行mc命令，在[moa-console](https://github.com/moajs/moa-console)中测试

```
➜  mongoose-console  mc
提醒:debug状态连接数据库:
mongodb://127.0.0.1:27017/mongoose-console-test

[2015-08-06 20:59:47.378] [INFO] [default] - undefined

[2015-08-06 20:59:47.379] [INFO] [default] - Welcome to the Moa console.
[2015-08-06 20:59:47.380] [INFO] [default] - undefined

Available Entity: 
  - Bson
  - Index
Moa> [mongoose log] Successfully connected to:  NaN
mongoose open success

undefined
Moa> .list
Available Entity: 
  - Bson
  - Index
Moa> Bson.find({},function(err,doc){console.log(doc)})
Moa> [ { _id: 55c35575b92da9b4fbeb3b26,
    user_name: 'alfred sang',
    __v: 0,
    created_at: Thu Aug 06 2015 20:39:17 GMT+0800 (CST) },
  { _id: 55c356f4d1b21737ffefb2d4,
    user_name: 'alfred sang',
    __v: 0,
    created_at: Thu Aug 06 2015 20:45:40 GMT+0800 (CST) },
  { _id: 55c356fb12e6f243ffb2c4dd,
    user_name: 'alfred sang',
    __v: 0,
    created_at: Thu Aug 06 2015 20:45:47 GMT+0800 (CST) },
  { _id: 55c35a3fa6474371030783a3,
    user_name: 'alfred sang',
    __v: 0,
    created_at: Thu Aug 06 2015 20:59:43 GMT+0800 (CST) } ]

(^C again to quit)
Moa> 
```


### example

```
➜  mongoose-console  node example.js 
提醒:debug状态连接数据库:
mongodb://127.0.0.1:27017/mongoose-console-test
[mongoose log] Successfully connected to:  NaN
mongoose open success
{ __v: 0,
  user_name: 'alfred sang',
  _id: 55c35a3fa6474371030783a3,
  created_at: Thu Aug 06 2015 20:59:43 GMT+0800 (CST) }
^C%        

```


全文完

欢迎关注我的公众号【node全栈】

![](/css/node全栈-公众号.png)
