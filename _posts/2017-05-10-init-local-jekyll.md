---
layout: post
title: "init local jekyll"
description: ""
category: 
tags: []
---

进到安装devkit目录，执行init，会生成config.yml


### ayfickle.github.io
a blog with jekyll

### How to install local jekyll evn?
#### win (http://rubyinstaller.org/downloads/)
- install python and add ptyhon to sys env
- install ruby and devkit fits installed ruby version
- init devkit
	- ruby dk.rb init

		> 进到安装devkit目录，执行init，会生成config.yml

	- ruby dk.rb install

		> 打开config.yml加上ruby安装目录在执行install。

- replace gem resourse
	- gem sources
	- gem sources --remove https://rubygems.org/
	- gem sources --a http://gems.ruby-china.org/
	- gem sources -c  

		> 清除原源缓存

	- gem sources -u

		> 更新缓存

	- gem install jekyll

- open jekyll file and run `jekyll server`
	
	> clone jekyll-bootstrap 
	gems: ["jekyll-sitemap"] and Gemfile -> ruby

- add new dairy file
	- gem install rake
	- _config.yml add permalink: /:categories/:year/:month/:day/:title 
	- create Rakefile
	- run rake post title="init local jekyll"

	> Rakefile 不可少
	如果是在windows的控制台，不执行gen install rake也是可以的，但是如果没有Rakefile的话，只能执行rake post，加上title参数则报错