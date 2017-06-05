---
layout: post
title: "codewars怀疑智商之路"
description: "some stupid moment"
category: code
tags: [codewars, javascript]
---

这大概就是一篇嫌弃史，不过希望能在嫌弃中成长起来。每每看到自己挖的一些坑，就真的怀疑脑子不够用，呐呐，这就来记录下吐槽，共勉。

### replace -- 06-05

嗷，交代下背景。在做一道题简述如下：

一个字符串如 "LY"，你可以在这个字符串任意一个位置添加任意个字符串 "fickle"，现在给你添加好的字符串，需推导出源字符串。

宝宝一看，哟，正则啊，妥妥的。为宝宝的机智点个赞。

然后宝宝写了个for循环这样写的：

```
if(arr[i] + arr[i+1] + arr[i+2] == 'fickle') {
	result.push('&')
}
else {
	result.push(arr[i]);
}
return arr.replace(/&+/g, ' ').trim();
```

嗷~~不要问我为什么这么蠢。非要把 'fickle' 换成 & ，不能让人家默默的保持原来的样子？所以，其实一句话就好：

```
return str.replace(/(fickle)+/g, ' ').trim();
```

### 待续...