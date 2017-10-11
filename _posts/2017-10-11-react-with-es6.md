---
layout: post
title: "React + ES6入门整理"
description: "react-create-app demo with es6"
category: front-end
tags: [react, es6]
---

刚接触React，不是第一次接触，很早之前了解过，那时候不求甚解，现在重新来过。哈哈哈，怕什么，只要在学习是吧！？就根据官方的Doc和ES6的写法总结了一下。

### 组件基础定义

```
class App extends Component {
  render() {
    return (
      <div className="App">
      ...
      </div>
    );
  }
}
```

这样定义了一个App的组件。可以直接使用：
`ReactDOM.render(<App />, document.getElementById('root'));`

### 设置默认的state和props

- 默认state

需要在组件的构造函数中设置：

```
class App extends Component {
  constructor(props) {
    super(props);
    this.state = {
      time: new Date().toLocaleTimeString(),
    };
  }

  render() {
    ...
  }
}
```

在`this.state`中定义state的默认值。相当于createClass里的`getInitialState`，写法如下：

```
var App = React.createClass({
  getInitialState: function() {
    return { time: new Date().toLocaleTimeString() }
  }
})
```

- 默认props

props默认不在组件的定义中设置：

```
class App extends Component {
  ...
}

App.defaultProps = {
  name: 'liuying'
}
```

同样，相当于在createClass的`getDefaultProps`中设置：

```
var App = React.createClass({
  getDefaultProps: function() {
    return { name: 'liuying' }
  }
})
```

### demo

- 计时器

主要是要明白计时器触发条件是在页面渲染之后，也就是`componentDidMount`状态函数是更新state。

```
class App extends Component {

  constructor(props) {
    super(props);
    this.state = {
      time: new Date().toLocaleTimeString(),
    };
  }

  clock() {
    this.setState({
      time: new Date().toLocaleTimeString()
    })
  }

  componentDidMount() {
    setInterval(() => this.clock(), 1000);
  }
  
  render() {
    return (
      <h2>{this.state.time}</h2>
    );
  }
}
```

> tips：额，关于函数调用，是需要手动绑定this的。
  `setInterval(() => this.clock(), 1000)` 等同于 `setInterval(this.clock.bind(this), 1000)`