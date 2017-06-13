---
layout: post
title: "jekyll比较常用的使用规则"
description: "usual rules for jekyll"
category: bolg
tags: [jekyll, blog, rules]
---

之前着实倒腾了JB（jekyll-bootstrap）一番，然而渐渐发现，基本上好像又都自己写了，所以便有了这个重构吧。

### 关于图片路径

鉴于之前没有看api，于是我在博文里加图片路径是绝对路径，例如：https://ayfickle.github.io/assest/themes... 这类的或者{{ ASSET_PATH }}/imgs/home/favicon.ico 之类的。JB里面的{{ ASSET_PATH }}是到assests/themes/ayfickle里面下的。

这样看下来确是不太优雅的，毕竟assests目录下有个imgs的文件夹存放图片就够了，放在主题下未免过深了。所以就去翻了jekyll的api，然后看到了有介绍：

`{ { site.url } }` 这个东东就用来定义根目录的，任何地方都可以放心的使用，这样一来就没有深层次的嵌套，感觉上还是不错的。于是我的路径都变成这样的了：{{ site.url }}/assets/imgs/codewars/compare.png 看起来是简洁了不少是吧。

哈哈，记得写的时候{{ }}括弧之间是木有空格的，我仅仅是为了显示才多了一个空格，不然会自动解释成当前的根目录。

### 关于目录显示文章简介

JB应该是内部把这个去掉了，如果引入JB的setup，那么不管怎么设置都是不会出现简述的。去掉之后，在 `_config.yml` 设置 `excerpt_separator: "\n\n"` 这个解释器，然后在文章 title 后加 `{ { post.excerpt | strip_html } }` 这样就可以的。

至此，基本上就完美的有了想展示在博客上的基本元素。

### 关于代码高亮

哦，这个问题我也还是懵逼的，没有找到好的方法，按照官方的写法，代码不能高亮但是可以显示行号。后续看看之后再做补充。

