---
layout: post
title: "关于 node-sass 安装失败的不完全解决方法"
description: "how to install node-sass successfully"
category: npm
tags: [npm, node-sass]
---

我司日常开发用的是Windows平台开发，所以这个不明不白安装node-sass不成功的事情是发生在Windows平台的，至于Linux和Mac没有实践。

### 经过

- 第一次 npm install

```
npm install
```

结束后，没有注意到报错，直接运行 `npm run dev` 哈哈哈，编译不通过。往前看，说是 `can not find module node-sass` 。嗯，这就是在说，我没有装成功啊喂。

- 第二次 npm install node-sass --save-dev

嗯。不错，报错是一模一样的。哦，当然，我是打开了vpn的，翻过了墙的。

- 第三次 cnpm install

先把node_modules文件夹删掉，然后重新使用cnpm来安装，这次报的错就是 `Cannot download "https://npm.taobao.org/mirrors/node-sass/v3.13.1/win32-x64-57_binding.node"` 呐呐，特意在浏览器打开这个链接，然后被告知 `Not Found` 。嗯，bingo，把这个版本改一改再安装就对啦。

- 第四次 反思

哈哈哈，再回头看了一下，这个 `v1.13.1` 这个版本就是没有了。所以之前npm安装也是木有问题的，已经测试过无误。

### 碰到提示 node-sass 安装不成功怎么处理最好？

#### 如果是clone别人的项目

- package.json文件里，删掉node-sass。

- 然后单独安装一次。如果还是不成功，那就只能考虑是自己网络的问题了。

- 归结到自己首次安装。

#### 自己项目首次安装

- 把npm的源换成cnpm：`npm install -g cnpm --registry=https://registry.npm.taobao.org`

- 离线安装

直接去相关的资源下载下来，检查下载的包名是否和模块名一样，不一样的话，修改后，解压到node-modules文件夹就可以啦。
