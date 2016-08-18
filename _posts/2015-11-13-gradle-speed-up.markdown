---
layout: post
title: "提速中的Gradle"
categories: problem
---

#### 提速方式一
* 砸钱，加内存，加固态 换电脑（有钱总是没错的）

#### 提速方式二
* org.gradle.daemon = true   //后台守护进程，在内存动态时时加载最新的data和code，为下次编译做准备 [doc](https://docs.gradle.org/current/userguide/gradle_daemon.html)
* org.gradle.parallel = true  //并行计算进行编译
* make gradle work in `offline` work mode //offline 不去检查更新dependencies
* set up large vm heap size: 2G

据说使用Android Studio自动帮忙做这些配置，所以效果不是很大

#### 提速方式三
* Disable Task gradle编译的时候，部分耗时较长的,将task disabled 当然不能影响正常运行(可以根据build/reports/profile查看具体的执行tasks)
  ```
     tasks.whenTaskAdded { task ->
    	if (task.name.startsWith(":zxing:") || task.name.startsWith(":share-lib:")) {
        	task.enabled = false
    	}
	}
  ```
  对于默认的tasks,好像基本不能disable(网上暂时没有查看)

#### 提速方式四
* Fackbook Buck https://github.com/facebook/buck (需要修改源文件)
* LayoutCast https://github.com/mmin18/LayoutCast(仅支持ART，暂不支持6.0，试用了下不是很好用,修改代码之后编译报错)

#### Refer
* http://akakanch.com/?p=138
* http://www.zhihu.com/question/36892290
* http://liaohuqiu.net/posts/speed-up-your-build/
