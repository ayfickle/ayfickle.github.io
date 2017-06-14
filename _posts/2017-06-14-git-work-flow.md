---
layout: post
title: "关于git使用的思考"
description: "some tips about git"
category: tools
tags: [tool, git, workflow]
---

突然想研究git log。起因是看到一张晒出来的git network graph，对比了下自己的graph，啧啧啧，怎一个乱字了得。

### git的前期困扰

起初接触git，是在一个小团队中，然后看了廖雪峰老师的[git教程](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/)，嗯，我的很多初识教程都来自廖老师和阮老师。

当时简单得多，我被告知几个常见的git命令：git clone、git pull、git branch、git checkout、git add、git commit、git diff、git merge、git push大概就是这几个命令。然后你会发现，就算只会这几个命令也完全可以满足日常的开发需求。但是，凡事总有但是，一旦你开始自己去管理约束整个git工作流，你就会发现这些不够用，准确的说，这些不能帮助你解决任何突发事件。

看了许多分支管理介绍，但是我还是没有一个很明确的方案来解决开发完成代码合并但是不上线的问题~！

### 常用到的git命令

- 自定义git命令

  git config --global alias.自定义命令 "git命令"。例如：

  git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"

  嗷，这个命令是极好的。可以查看你的整个git network flow，非常的棒。

- 增删改查git库

  git remote -v