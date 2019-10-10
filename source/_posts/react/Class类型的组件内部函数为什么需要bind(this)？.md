---
title: Class类型的组件内部函数为什么需要bind(this)？
date: 2019-09-18 00:00:00
categories:
  - react
tags:
  - 组件
  - this
cover: >-
  https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1570615514153&di=6f99e51380c6212468e4565b6321a633&imgtype=0&src=http%3A%2F%2Fpic4.zhimg.com%2Fv2-38bdac71902e51febd1ab576a32c0616_1200x500.jpg
---

### bind(this)的原因

- 在`JavaScript`中，`class`内定义的方法默认情况下不会绑定`this`，所以我们要使用bind()手动绑定this，使this时刻指向组件本身

### 其他绑定this的方法

1. 定义时绑定
    ```javascript
        // 此语法确保 `handleClick` 内的 `this` 已被绑定。
        // 注意: 这是 *实验性* 语法。
        handleClick = () => {
        console.log('this is:', this);
        }
    ```
2. 调用时绑定
    ```javascript
        render() {
            // 此语法确保 `handleClick` 内的 `this` 已被绑定。
            return (
                <button onClick={(e) => this.handleClick(e)}>
                Click me
                </button>
            );
        }
	```

### 推荐阅读
- [MDN bind 文档](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)
- [React handle event](https://reactjs.org/docs/handling-events.html)
- [Understanding JavaScript Bind ()](https://www.smashingmagazine.com/2014/01/understanding-javascript-function-prototype-bind/)

