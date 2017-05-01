---
layout: post
title:  hyperlink vs rest
categories: Microservice
keywords: Learn
description: 是时候学一点关于web的理论了
---

今天看到一句话
> JSON has no built-in support for hyperlinks, which are a fundamental building block on the Web.

可能是web的理论太少了, 觉得理解不了，于是查了下。

这个缺陷大致意思是，用Rest提供API，你不知道一个API和其他的API有什么关联，用户都要去查文档。
Rest中相关资源的依赖和链接，如何管理，如何表达，怎么做标准化？

HAL(Hypertext Application Language) 解决这个问题，并加上了Links和embedded resources.

```
{
     "_links": {
       "self": { "href": "/orders/523" },
       "warehouse": { "href": "/warehouse/56" },
       "invoice": { "href": "/invoices/873" }
     },
     "currency": "USD",
     "status": "shipped",
     "total": 10.20
   }

   "_embedded": {
     "category": {
       "_links": {......},
       "state": {......}
     }
   }
```

疑问，这玩意跟oData特别地像，所以oData是实现了hyper link的？
可是，平时做事情的时候，我是把这部分数据给过滤掉的。
不过依然看到它带来的一点好处是，比如对于user，我知道它的manager的链接，以及user和什么人有关系。
但是我调用oData，一样要看文档。
