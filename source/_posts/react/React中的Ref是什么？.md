---
title: React中的Ref是什么？
date: 2019-09-18 00:00:00
categories:
  - react
tags:
  - 组件
  - ref
cover: >-
  https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1570615514153&di=6f99e51380c6212468e4565b6321a633&imgtype=0&src=http%3A%2F%2Fpic4.zhimg.com%2Fv2-38bdac71902e51febd1ab576a32c0616_1200x500.jpg
---

### ref是什么

- ref是React提供的`用来操纵React组件实例`或者`DOM元素`的接口

### 如何使用ref

- `你不能在函数组件上使用 ref 属性，因为他们没有实例`
- 使用：
    1. 使用 `React.createRef()` 创建
    2. 将ref属性附加到React元素上
        ```
        class MyComponent extends React.Component {
            constructor(props) {
                super(props);
                this.myRef = React.createRef();
            }
            render() {
                return <div ref={this.myRef} />;
            }
        }
        ```   
    3. 使用current属性来访问DOM上绑定的对象
        - 当 `ref` 属性用于 HTML 元素时，构造函数中使用 `React.createRef()` 创建的 `ref` 接收底层 DOM 元素作为其 `current` 属性。
        - 当 `ref` 属性用于自定义 class 组件时，`ref` 对象接收组件的挂载实例作为其 `current` 属性。

### ref的应用场景

- 管理焦点，选择文本或媒体播放。
- 触发式动画。
- 与第三方DOM库集成。

### 推荐阅读
- [React refs and dom](https://zh-hans.reactjs.org/docs/refs-and-the-dom.html)
- [React 重温之 Refs](https://segmentfault.com/a/1190000015113359)
- [React ref 的前世今生](https://zhuanlan.zhihu.com/p/40462264)
