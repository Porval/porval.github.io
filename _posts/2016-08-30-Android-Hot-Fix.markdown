---
layout: post
title:  "Android Hot Fix"
date:   2016-08-30 02:28:00
categories: problem
---

Android对热修复如饥似渴的地步，今天有空来过一下Android大厂的Hot Fix方案

### And Fix
* https://github.com/alibaba/andfix

* [原理](http://w4lle.github.io/2016/03/03/Android%E7%83%AD%E8%A1%A5%E4%B8%81%E4%B9%8BAndFix%E5%8E%9F%E7%90%86%E8%A7%A3%E6%9E%90/) 在native动态替换方法java层的代码，通过native层hook java层的代码。

* 由于在native层的操作，导致在国产机上运行效果并不理想，同时是对class的方法替换，不能修改变量以及对初始化有依赖的类也会有问题

* 由于阿里巴巴已经放弃该方案，传言内部有2.0版本，导致And Fix基本被废弃了

### Rocoo Fix
* https://github.com/dodola/RocooFix

* RocooFix是基于Qzone热修复方案的实践, 与之相似的还有Nuwa, HotFix.

* RocooFix的实现原理是，通过每个apk运行时的classLoader可以加载多个.dex文件，当重复类出现在多个.dex文件中时，读取靠前.dex中class。因此当apk获取到patch的时候，将.dex插入到当前apk的classloder即可 [原理](http://bugly.qq.com/bbs/forum.php?mod=viewthread&tid=16)

* 从原来来看，RocooFix方案以类的单位来修复, 不支持替换资源文件，so文件等,由于是分包的情况下，会影响启动速度(貌似还挺严重的)

### Tinker
* https://github.com/zzz40500/Tinker_imitator

* Tinker的原理是修复版本和旧版本的dex差异生成patch文件，通过生成patch文件在手机端生成新版的全部dex,加载新的dex来实现打补丁的功能点  [原理](http://mp.weixin.qq.com/s?__biz=MzAwNDY1ODY2OQ==&mid=2649286306&idx=1&sn=d6b2865e033a99de60b2d4314c6e0a25&scene=1&srcid=0811AOttpqUnh1Wu5PYcXbnZ#rd)

* Tinker优化了差异patch生成算法，致使优化patch文件包大小

### Reference
* http://gold.xitu.io/entry/57bfecd46be3ff0058245db9
* http://bugly.qq.com/bbs/forum.php?mod=viewthread&tid=16
* http://my.oschina.net/853294317/blog/308583
* http://www.kymjs.com/code/2016/05/08/01
* http://w4lle.github.io/2016/03/03/Android%E7%83%AD%E8%A1%A5%E4%B8%81%E4%B9%8BAndFix%E5%8E%9F%E7%90%86%E8%A7%A3%E6%9E%90
* http://dev.qq.com/topic/57ad7a70eaed47bb2699e68e
* http://mp.weixin.qq.com/s?__biz=MzAwNDY1ODY2OQ==&mid=2649286306&idx=1&sn=d6b2865e033a99de60b2d4314c6e0a25&scene=1&srcid=0811AOttpqUnh1Wu5PYcXbnZ#rd
* http://dev.qq.com/topic/57ad7a70eaed47bb2699e68e
