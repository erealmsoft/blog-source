---
title: React中propsTypes类型检测的用法
tags:
  - props
  - 类型检测
cover: >-
  https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1570615514153&di=6f99e51380c6212468e4565b6321a633&imgtype=0&src=http%3A%2F%2Fpic4.zhimg.com%2Fv2-38bdac71902e51febd1ab576a32c0616_1200x500.jpg
categories:
  - react
date: 2019-09-27 00:00:00
---

### propsTypes的作用
- 在React中，propsType是用来对组件props做类型检查的

### 用法
1. 引入校验模块 `prop-types`
2. 定义Component，然后给Component上面挂propsType属性

### 举个栗子
```
class Greeting extends React.Component {
	render() {
	    return (
	      <h1>Hello, {this.props.name}</h1>
	    );
	  }
}
Greeting.propTypes = {
	name: PropTypes.string
};
```
