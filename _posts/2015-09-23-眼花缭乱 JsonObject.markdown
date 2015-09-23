---
layout: post
title: "眼花缭乱 JsonObject"
categories: problem
---

###JSONObject vs JsonObject

两个类很像，不注意写就容易同时出现在code中，导致代码混乱。
添加上包名就比较容易区别些

org.json.JSONObject vs com.google.gson.JsonObject

搞清楚两者的关系，需要先清楚Json是什么

###Json是什么

Json是一种轻量级、独立于语言便于交互的数据格式.

```java
   {
      "id":1,
      "title":"xxx",
      "count":2
   }
```

[详见](http://www.json.org/)  

###JSON libs
所以基于Json数据格式的Java实现有很多,以下列举了一些比较常用的

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
