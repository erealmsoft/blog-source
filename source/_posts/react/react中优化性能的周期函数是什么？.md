---
title: react中优化性能的周期函数是什么？
date: 2019-09-16 00:00:00
categories:
  - react
tags:
  - 生命周期
  - 性能优化
cover: >-
  https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1570615514153&di=6f99e51380c6212468e4565b6321a633&imgtype=0&src=http%3A%2F%2Fpic4.zhimg.com%2Fv2-38bdac71902e51febd1ab576a32c0616_1200x500.jpg
---

### react中优化性能的周期函数

- `shouldComponentUpdate(nextProps, nextState)`
- 它是决定react组件什么时候能够不重新渲染的函数，默认返回值为true。也就是说，默认每次更新的时候都要调用所有的生命周期函数，包括render函数，重新渲染。

### 如何使用它

- 可以通过对新旧props及state的比较来返回true/false，参与决定该组件是否需要被重新渲染（官方文档中提到`shouldComponentUpdate`不是决定是否渲染组件的唯一条件，还与返回的 React 元素是否相同有关）

### 推荐阅读

- [官方文档（避免调停）](https://react-1251415695.cos-website.ap-chengdu.myqcloud.com/docs/optimizing-performance.html)

