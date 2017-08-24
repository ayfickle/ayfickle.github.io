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

当时简单得多，我被告知几个常见的git命令：git clone、git pull、git branch、git checkout、git add、git commit、git fetch、git diff、git merge、git push大概就是这几个命令。然后你会发现，就算只会这几个命令也完全可以满足日常的开发需求。但是，凡事总有但是，一旦你开始自己去管理约束整个git工作流，你就会发现这些不够用，准确的说，这些不能帮助你解决任何突发事件。

### git分支管理

综合许多关于分支以及工作流的文章的介绍，我了解到的皮毛是这样的：

- master一般作为主分支，只有在版本发布时才进行更新；

- develop作为开发分支，可以随时更新，但不在分支上做开发修改；

- 当新需求需要开发时，新建feature分支，开发完成后合到develop分支并删除分支；

- 测试时，从develop拉出release分支，类似于二次开发，完成后，合并到develop分支；

- 准备就绪，将develop合并到master分支进行版本发布；

- 线上出现问题时，从master拉出debug分支修复bug，完成后，合并到master和develop并删除分支。

    示例图如下：

    ![工作流示例图]({{ site.url }}/assets/imgs/git/workflow.png)

这是整个的开发方向。

然而大部分时间都是协作开发，你需要做的操作要多得多。

### 只是个人理解

- 模块合作开发

  两个及以上的人合作开发的流程如下：

  - A开发完成后，新建并推送到远程分支branchA，B拉到本地继续开发；

  - A再进行开发时，推送到远程前，需要git fetch远程分支，并git diff查看远程与本地的不同，确定后，再合并推送；

  - 知道开发完成，合并到主分支，并删除远程分支。

在开发中，秉承分支开发完成即删除，多人开发中，提交前先更新远程分支内容到本地比较，再合并新的开发内容并推送，按照这个原则，开发过程中很少会有大的问题。

### git工作台

推荐一个名为SourceTree的工具。可是很清楚的看得到整个工作流，尽量让你的工作流分支整洁不发叉。
稍后补充说明~

### 一些疑问

在实际工作中，一般会有固定的发布周期，两周一次或者更加频繁的一周一次。开发的实际进度会远超上线的速度，不在计划内的上线内容可以在feature-future分支上开发，在计划内的需求开发完成后并且测试通过，但是，临上线的时候砍掉了这个需求，这时候该怎么处理？版本回退还是直接删代码，额，删代码这个肯定不靠谱，删错了就要呵呵哒了。

前期我的解决方法是，一个需求一个分支，测试时，分支合到测试分支，上线的最后一刻，才把确定的上线需求合并到生产分支上再上传代码。这样就是，每次上线，都要等到很晚，等后台上线完成并确认无误再更新，对于前后端分离来讲，这是个耗时不讨好的动作。

但是，没有想到更好地对于这种临时不上线内容的管理办法，也许是理解git还停留在比较浅显的层次。最近看了不少的文章，还是没有看出所以然，等待解决方案中。。。

### 常用到的git命令

- 自定义git命令

  git config --global alias.自定义命令 "git命令"。例如：

  git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"

  嗷，这个命令是极好的。可以查看你的整个git network flow，非常的棒。

- 增删改查git库

  git remote -v

- 设置本地分支追踪远程分支

  git branch --set-upstream local_branch origin/remote_branch

  另外，如果你本身已经将本地分支推送到远程，例如：

  git push origin remote_branch

  这不会自动追踪远程分支，那么每次git操作，仍然需要制定远程分支名。当时还是可以设置的：

  git push --set-upstream origin remote_branch

