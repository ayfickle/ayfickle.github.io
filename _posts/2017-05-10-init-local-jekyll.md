---
layout: post
title: "倒腾jekyll+github做个简单的博客"
description: "init local jekyll"
category: blog
tags: [jekyll, blog, DIY]
---

倒腾了个github上的blog。然后顺手配了下windows的本地jekyll环境，碰到一些坑，写出来共享下。

### create a github blog

在github上创建博客，有两种形式。
- 直接在github上create new repository.命名为username.github.io
  clone到本地，按照jekyll的目录结构进行配置。
- 先安装本地jekyll环境，直接用jekyll初始化再提交到github上。
 `对于这两种，陆先森认真的跟我说其实就是一种。但是，我不听，我不听，乖巧.jpg`

### How to create?

#### just DIY

如果全部要手动折腾的话，可以参考阮一峰老师的[搭建一个免费的，无限流量的Blog----github Pages和Jekyll入门](http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html)，照着走下来，可以快速看到自己的blog诞生。

当时在这里遇到一个坑，直接在sublime里面设置头信息一直不识别，后面发现是---编码的问题，需要设置成无BOM格式的utf-8格式。然后就是post的文件命名格式，也被坑了一把，当然是因为刚开始没有好好看jekyll的api啦，不过还是建议本地环境搭好，直接生成多棒！

#### just try

好的，没啥技术含量的正文开始了。

##### step1 install

既然是本地环境，那肯定是要安装的咯。要安装三个，Python，Ruby和devkit。

要注意两点：
- python安装后需要手动配置环境变量。
- devkit需要选择已安装ruby相对应的版本，[下载点这](http://rubyinstaller.org/downloads/)。

##### step2 init

- init devkit
	- 进到安装devkit目录，执行 **ruby dk.rb init** ，会生成config.yml
	- 打开config.yml加上ruby安装目录执行ruby dk.rb install

  devkit初始化完成

- 替换 gem 源
  至于为什么需要这个步骤，哈哈哈，自然都是因为那墙，不换根本gem install不起来。命令如下：
	- gem sources
	- gem sources --remove https://rubygems.org/
	- gem sources --a http://gems.ruby-china.org/
	- gem sources -c 清除原源缓存
	- gem sources -u 更新缓存

- 安装jekyll => gem install jekyll

- 运行jekyll => jekyll server
	> 这里我才开始clone了jekyll-bootstrap的项目，刚开始跑不起来。主要是jekyll-sitemap和Gemfile的原因，这里面牵扯到ruby，宝宝决定不去深究。如果想看看，我删掉一些配置，愉快的server成功，可以戳这里[jekyll-bootstrap](https://github.com/ayfickle/jekyll-bootstrap).

- 添加post博文
	- gem install rake 这个主要是git bash没有rake命令，需要安装。
	- 在_config.yml 添加配置 permalink: /:categories/:year/:month/:day/:title 
	- 新增 Rakefile 配置项参考[这里](https://github.com/ayfickle/ayfickle.github.io/blob/master/Rakefile)
	![Rakefile](https://ayfickle.github.io/assets/themes/ayfickle/imgs/init/step1.png)
	> Rakefile 不可少
	如果是在windows的控制台，直接rake post会创建，但是加上title参数则报错，又跟ruby有关，被跳过。

	- 运行 rake post title="init local jekyll"
	![create new](https://ayfickle.github.io/assets/themes/ayfickle/imgs/init/step3.png)

  到这里，已经初始化成功了，肯定是没有什么问题了吧。很好，下面就是自己设计blog的样式了。但是本宝宝审美设计方面弱到爆，只能丑丑的摆在那，将就将就看着。

  既然排版设计方面憋不出来字，那我来唠叨唠叨现在理解到的有关jekyll的某些东西？

#### about jekyll

##### _config.yml

比较有效的配置：
- permalink: /:categories/:year/:month/:day/:title 

  作为rake post title 的格式
- excerpt_separator: "\n\n"

  可以在列表加上{{ post.excerpt | strip_html }}截取文章的第一段落

##### 头信息

rake post自动生成头信息
![title config](https://ayfickle.github.io/assets/themes/ayfickle/imgs/init/step2.png)
- layout 是 当前页面引用的布局文件
- category 类别
- tags 所属标签
- 还可添加 author 等自定义配置，在文章中用{{ page.author }}引用其值。

### 最后

突然发现写一篇稍微有点用的东西出来很是不简单，一不小心就啰里啰嗦没有重点，或者是一笔带过，看者摸不着头脑。

写的时候才感受到，对makedown的语法不熟练，写着写着就要看看怎么用怎么写，而且makedown的解释器还不尽相同，着实难受。但是，不管怎样，这篇难产了许久的博文总算是出来了，有了第一个就自然会有接下来的第二三四个，哈哈哈，继续写起来。

啊，等我晚些再来完善这篇处女作，现在就到这吧。