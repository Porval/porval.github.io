---
layout: post
title:  "Post To Maven Center"
date:   2016-08-18 11:00:00
categories: design
---

老文贴过来

# 前言
===
当在github上看到其他第三方库时，总是会出现例如

```
    dependencies {
        compile 'com.github.porval:infiniteindicator:1.0.0'
    }
```

这样神奇的代码，简单添加到自己的build.gradle中就可以使用这个第三方库了.

实际的工作流程是这样的

* Android lib作者将已编译好的jar或者aar,上传到了Maven_Center
* 用户引用第三方lib时在本地的app中build.gradle声明被引用的lib(如上)
* app在编译的时候将会自动到Maven Center中下载相关的lib

这里主要讲的是Android lib如何将已编译打包的jar或者aar上传至Maven_Center发布，另其他app可以引用


# 基础概念
===
* _Maven Center_ 全世界java lib通常存储在一个较大的节点（repository）就是Maven Center.类似于Node.js中的NPM 或者Python中的PyPI 可以通过http://search.maven.org搜索已在Maven Center中已发布的java lib


# 发布流程
===

#### 注册
-----
1. 注册 [Sonatype](https://issues.sonatype.org/secure/Signup!default.jspa)(如果你有账号就不需要再注册)

2. [创建问题](https://issues.sonatype.org/secure/CreateIssue.jspa?issuetype=21&pid=10134)创建时，需要添加project url(github地址之类的)、project依赖以及相关的描述信息.确认**group_id**(合法的groud id必须包含一个.,例如com.github._yourname_),在1-2个工作日后工作人员会处理issue,你将会收到邮件
确认收到邮件之后，才能上传

#### 配置gpg(已配置可略过)
---
1. 安装之后，生成gpg key

```
$ gpg --gen-key
```

2.生成之后找到你的gpg id

```
$ gpg --list-keys
```
第一行中显示格式为XXXXX/YYYYYYYY \<date> YYYYYYYY的值就是你的id

3.发送到服务器

```
$ gpg --keyserver hkp://keyserver.ubuntu.com --send-keys YYYYYYYY
$ gpg --keyserver hkp://pgp.mit.edu --send-keys YYYYYYYY
```
4.确定发送成功

```
$ gpg --keyserver hkp://pgp.mit.edu --search-keys porval@gmail.com# Use your email
```

#### 配置gradle
---
1. 参考[gradle-mvn-push](https://github.com/chrisbanes/gradle-mvn-push)


#### 上传lib
----
1.配置好gradle,最后一步调用（上传文件）
```
$ gradle clean build up uploadArchives
```

2.如果gradle.propertities中配置VERSION_NAME=1.0.0-SNAPSHOT,lib将会上传到[SNAPSHOT](https://oss.sonatype.org/content/repositories/snapshots/com/felipecsl/android/)站点，这里不是线上正式环境(据说这一步不能略过)

3.如果gradle.propertities中配置VERSION_NAME=1.0.0(不带后缀-SNAPSHOT),lib将会上传到
[OSSRH web UI](https://oss.sonatype.org/#welcome),登录查看你上传的lib,一般在最后出于opened状态，选用之后点击closed按钮（closed可能失败，之前的gpg sign以及包依赖等问题）

4.closed成功之后，可点击release按钮,之后你的上传的lib将会被同步到Maven Center中，可能需要隔天才能在http://search.maven.org搜索出来。这样其他project就可以引用你的lib。发布成功之后请在[JIRA](https://issues.sonatype.org/secure/Signup!default.jspa)中你创建issue回复，方便处理tickets

# 参考
===
* http://zserge.com/blog/gradle-maven-publish.html
* https://github.com/chrisbanes/gradle-mvn-push
* http://felipecsl.com/blog/2013/12/06/publishing-an-android-library-to-maven-central/
