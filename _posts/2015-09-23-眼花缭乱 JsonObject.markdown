---
layout: post
title: "眼花缭乱 JsonObject"
categories: problem
---

#眼花缭乱 JsonObject

###json是什么

json是一种轻量级、独立于语言便于交互的数据格式.

```java
   {
      "id":1,
      "title":"xxx",
      "count":2
   }
```

[详见](http://www.json.org/)  

###JSON libs
* [orj.json](https://github.com/douglascrockford/JSON-java)
  java古老常用的package,android sdk中自带.JsonObject常用的方法比较简单实用
  最大的缺点是需要读取整个字符串才能解析.

* [Gson](https://github.com/google/gson)
  Gson（又称Google Gson）是Google公司2008年发布的一个开放源代码的Java库，主要用途为序列化Java对象为JSON字符串，或反序列化JSON字符串成Java对象.

  PS:Gson包中的JSONObject用起来不爽

* [jackson](http://www.eoeandroid.com/thread-173165-1-1.html) 据说效率比较gson更快一些，但是考虑到android app集成lib需要考虑包的大小，不推荐使用.(最新版本已经达到了1.1M)

###refrence
* https://en.wikipedia.org/wiki/Gson
* http://stackoverflow.com/questions/7935078/performance-and-usability-comparison-of-android-json-libraries
* https://groups.google.com/forum/#!topic/google-gson/XPQerLWrgSI
