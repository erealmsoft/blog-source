---
title: getDerivedStateFromError() 和 componentDidCatch() 有什么区别
date: 2019-09-23 00:00:00
categories:
  - react
tags:
  - 错误处理
cover: >-
  https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1570615514153&di=6f99e51380c6212468e4565b6321a633&imgtype=0&src=http%3A%2F%2Fpic4.zhimg.com%2Fv2-38bdac71902e51febd1ab576a32c0616_1200x500.jpg
---

### 这两个函数是什么

- 它们是React16引入的一个新概念 —— `错误边界`
    - 过去，组件内的 JavaScript 错误会导致 React 的内部状态被破坏，并且在下一次渲染时产生可能无法追踪的错误。这些错误基本上是由较早的其他代码（非 React 组件代码）错误引起的，但 React 并没有提供一种在组件中优雅处理这些错误的方式，也无法从错误中恢复。
    - 错误边界是一种 React 组件，这种组件`可以捕获并打印发生在其子组件树任何位置的 JavaScript 错误，并且，它会渲染出备用 UI`，而不是渲染那些崩溃了的子组件树。错误边界在渲染期间、生命周期方法和整个组件树的构造函数中捕获错误。
    - 需要注意以下几点：
        1. 错误边界`无法`捕获以下场景中产生的错误
            - 事件处理
            - 异步代码
            - 服务端渲染
            - 它自身抛出来的错误
        2. 只有class组件才可以成为错误边界组件
        3. 错误边界仅可以捕获其子组件的错误，它无法捕获自身错误。如果一个错误边界无法渲染错误信息，则错误会冒泡至最近的上层错误边界

### 它们分别的作用是什么

- `getDerivedStateFromError()` ：渲染备用UI
- `componentDidCatch()` ：打印错误信息

### 触发场景

- 如果一个 class 组件中定义了 static getDerivedStateFromError() 或 componentDidCatch() 这两个生命周期方法中的任意一个（或两个）时，那么它就变成一个错误边界。当抛出错误后，使用 static getDerivedStateFromError() 渲染备用 UI ，componentDidCatch() 打印错误信息

### 它们的区别

| 类别        | getDerivedStateFromError | componentDidCatch |
| ------      | ------------------------ | -----------------   |
| 调用时间     | 渲染阶段调用              | 会在“提交”阶段被调用 |
| 执行其它操作 | 不可以                    | 可以                |
| 参数        | err                       | err,info          |

### 推荐阅读

-   [whats-the-difference-between-getderivedstatefromerror-and-componentdidcatch](https://stackoverflow.com/questions/52962851/whats-the-difference-between-getderivedstatefromerror-and-componentdidcatch)
-   [官方文档](https://zh-hans.reactjs.org/docs/react-component.html#static-getderivedstatefromerror)