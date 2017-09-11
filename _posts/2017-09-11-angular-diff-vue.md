---
layout: post
title: "What's different with angular and vue"
description: "some diffs between angular and vue"
category: front-end
tags: [angualar, vue, diff]
---

用Angular边学边做了3个比较大的单页应用了，最近在看Vue。因为入门的基础太像，不自觉的会比较这两者，也就整理了些这两个的一些比较点。

### 启动

- Angular

Angular通过 bootstrap 手动启动应用。

`angular.bootstrap(element, [modules], [config]);`

> element(必需)。要启动angular的根节点，一般为document，也可以是其他的的html的dom
  modules(数组，可选)。依赖的模块
  conifg(object,可选)。配置项，默认为false,是否开启辅助debug

然后，我在写 angular+require 的指令demo时，主要就是用的这种方式。具体可以查看[angular-directive](https://github.com/ayfickle/angular-directive/blob/master/app/script/main.js)

- Vue

Vue应该不算是自启动，而是把vue的实例手动挂载到某个DOM上。

`var app = new Vue({ ... });`

`app.$mount('#id');`

这种主要是需要延迟挂载，实例中没有el属性，则实例尚未挂载到DOM。在需要挂载时，通过 vm.$mount() 方法来挂载。

### 数据绑定

- Vue

Vue 除了 v-model 数据双向绑定，也有在各元素上的属性绑定。

需要注意的是，属性绑定需要使用v-bind，例如：v-bind:class。`v-bind:attr` 可简写为：`:attr`

- Angular

Angular 的绑定则宽泛的多，不管是值绑定还是属性绑定，均可采用 `{ { val } }` 绑定。