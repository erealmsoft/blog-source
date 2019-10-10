---
title: 应该在React组件的何处发起Ajax请求？
tags:
  - 组件
  - Ajax请求
cover: >-
  https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1570615514153&di=6f99e51380c6212468e4565b6321a633&imgtype=0&src=http%3A%2F%2Fpic4.zhimg.com%2Fv2-38bdac71902e51febd1ab576a32c0616_1200x500.jpg
categories:
  - react
date: 2019-09-25 00:00:00
---

- 应该在componentDidMount函数中发起Ajax请求
- 原因
    - 它在整个生命周期中只执行一次，避免了重复请求数据的情况
    - 如果在挂载组件之前获取到了数据请求结果，并在该组件上调用setState，这将不起作用，在componentDidMount中发起网络请求将保证这个组件可以更新
