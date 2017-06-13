---
layout: post
title: "codewars怀疑智商之路-入门级"
description: "some stupid moment"
category: code
tags: [codewars, javascript]
---

这大概就是一篇嫌弃史，不过希望能在嫌弃中成长起来。每每看到自己挖的一些坑，就真的怀疑脑子不够用，呐呐，这就来记录下吐槽，共勉。

### replace -- 06-05

嗷，交代下背景。在做一道题简述如下：

一个字符串如 "LY"，你可以在这个字符串任意一个位置添加任意个字符串 "fickle"，现在给你添加好的字符串，需推导出源字符串。

小六一看，哟，正则啊，妥妥的。为小六的机智点个赞。

然后小六写了个for循环这样写的：

```javascript
if(arr[i] + arr[i+1] + arr[i+2] == 'fickle') {
	result.push('&')
}
else {
	result.push(arr[i]);
}
return arr.replace(/&+/g, ' ').trim();
```

嗷~~不要问我为什么这么蠢。非要把 'fickle' 换成 & ，不能让人家默默的保持原来的样子？所以，其实一句话就好：

```javascript
return str.replace(/(fickle)+/g, ' ').trim();
```

### first word to uppercase

给定字符串，然后把每个单词的首字母全部大写...

两种比较好的解决方法：

- 通过map遍历 

	```javascript
	String.prototype.toJadenCase = function () { 
		return this.split(" ").map(function(word){
			return word.charAt(0).toUpperCase() + word.slice(1);
		}).join(" ");
	}
	```

- 正则 --- 正则大法好

	```javascript
	String.prototype.toJadenCase = function () {
	  	return this.replace(/(^|\s)[a-z]/g, function(x){ return x.toUpperCase(); });
	};
	```

### 中场休息

呐呐，做这种东西，莫过于一两分钟后看到这种结果啦。

![success]({{ site.url }}/assets/imgs/codewars/success.png)

但是！随之而来的就是深深地嫌弃和打击，不过还好，对基础的长进还是很有帮助的。

![success]({{ site.url }}/assets/imgs/codewars/compare.png)

### some tips

{% highlight javascript linenos %}
if(a === b) return true|false;
eqals to
return a === b;
{% endhighlight %}

it's embarrassing, right ?

`这是一些有关思路和实现的吐槽`

- 给定四个方向，NORTH SOUTH EAST WEST 以及一个包含这四个反向的数组，找最短路径（最短路径不是特别准确）。最终目的就是消除所有相对的方向。

  小六琢磨一番后，思路是这样的：用一个result数组存放不能被抵消的方向元素，用result的最后一个元素去比对。然后，实现如下：

  ```javascript 
  function dirReduc(plan) {
  var opposite = {
    'NORTH': 'SOUTH', 'EAST': 'WEST', 'SOUTH': 'NORTH', 'WEST': 'EAST'};
  return plan.reduce(function(dirs, dir){
      if (dirs[dirs.length - 1] === opposite[dir])
        dirs.pop();
      else
        dirs.push(dir);
      return dirs;
    }, []);
  }
  ```

  或者小六一开始倒是想到正则做，可无奈正则太渣，只能放弃。贴上一段正则的解法：

  ```javascript
  function dirReduc(arr) {
  	var str = arr.join(''), pattern = /NORTHSOUTH|EASTWEST|SOUTHNORTH|WESTEAST/;
  	while (pattern.test(str)) str = str.replace(pattern,'');
  	return str.match(/(NORTH|SOUTH|EAST|WEST)/g)||[];
  }
  ```

  小六表示很惭愧，没有很好处理方向比对，然后没有好好利用数组的一些方法。这些方法都是看了好几遍，但是碰到实际问题总是用不起来，每次都感觉自己好像又实现了一个不是很健壮的数组方法，戳心。也是以此为记，慢慢挣脱每次看到数组就是for循环的习惯，把它本身的东西慢慢融会贯通。

- 食谱做菜，食谱由若干材料名字和数量组成的对象，已有的食材也是一个对象，那么，根据食谱最多能做成多少菜呢？

  那么，作为对象有个很好的for...in循环、此处in则是对象里每个元素的key值，真的很棒。

  ```javascript
  function cakes(recipe, available) {
	  var numCakes = [];
	  for(var key in recipe){
	    if(recipe.hasOwnProperty(key)){
	      if(key in available){
	        numCakes.push(Math.floor(available[key] / recipe[key]));
	      } else{
	        return 0;
	      }
	    }
	  }
	  return Math.min.apply(null, numCakes); 
  }
  ```

