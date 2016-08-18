---
layout: post
title:  "MVC MVP MVVM"
date:   2016-08-17 10:00:00
categories: design
---

2015在google I/O大会上出现的Binding Data框架是基于MVVM设计模型来实现，加上之前已经比较火的MVP模式和传统的MVC模式，就有点绕晕了，三者放在一起对比下就比较清晰了.

### 设备端的开发
首先需要明确下，设备端开发经常要处理的逻辑，这样对于理解三种模式来说比较方便一些.(由于个人比较熟悉Android，所以以Android为模板，其他设备端可能有出入，请谅解)

1. 用户操作页面
2. 页面提交数据，进行逻辑处理
3. 数据处理完成，存储到数据源
4. 数据源数据更新，发出通知
5. 页面收到通知，重新获取数据
6. 渲染页面

以上差不是设备端开发要处理的5个基本逻辑，其中在某个简易场景下，不需要用到所有的逻辑（如，刚进入页面渲染的时候，只需要获取数据，又如，统计事件一些后台的操作就不需要页面显示，只需要3，4即可）

对于不同的设计模式来讲，只是将以上的逻辑封装到不同的抽象模块中来实现，模块之间的信息通道也不同。

### MVC
* MVC中m和c的分离比较清晰，v和c的分离就比较模糊。刚出现的时候，这个设计是为了在pc的excel 文档软件对于相同数据源下，不同view的展示
* 在Android 由于xml的View视图功能太弱，需要在activity中处理View的业务逻辑（可见不可见，重新刷新等）传统activity就变得过于庞大了
* 由上可见Activity就需要2、3、5、6的逻辑，往往出现上千行代码

### MVP
* MVC和MVP最大的差别在于MVP中将Activity当做纯粹的View来处理,Activity只是负责设置layout以及暴露对应的view操作接口给P层，让P层可以操作。
* P层来完成业务逻辑控制页面如何渲染 将原来2、3、5的逻辑剥离出来
* 目前看来MVP很完美，但是在实际操作中，对应一个V需要对应一个P,许多较多的app代码复用性太差，导致MVP框架并没有非常流行
* 基于这样的弱点，google大神又进行了优化推出[Android-Clean](https://github.com/googlesamples/android-architecture/tree/todo-mvp-clean/)框架, 有兴趣的同学可以看下

### MVVM
基于MVC中V相对较弱的特点，加强下V的能力是否可以优化Android现有的代码框架
所以有了mvvm设计模式

* ViewModel是MVVM中的核心,View层的渲染逻辑（比如view是否显示，textView显示什么字)通过ViewModel数据模型来表达。在View端根据对应的ViewModel来决定如何渲染，在controller层来操作ViewModel实例通知View渲染 View的数据更改了通过ViewModel告之Controller进行处理 ViewModel类并不是纯粹的Entity,对于简单的逻辑还是可以写入View,减轻了Controller的处理（比如editor 判空处理）
* 在个人看来MVVM将View中的渲染逻辑实例化，controller层操作更加简洁，且对于View来说复用性也很强
* google 通过databinding 框架来实现VM Activity来处理对应的业务逻辑。databinding目前只能单向绑定，View变化不能直接更改ViewModel实例数据



### 总结
目前来databinding模式还在开发阶段，有很多坑需要踩，希望google这个项目不要烂尾。从个人角度来说databinding还是挺实用，可以很大程度上理清代码结构。



### Reference
* https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93presenter
* http://www.jianshu.com/p/bd24c38eeb3c
