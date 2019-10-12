---
title: a链接与 router 中 link 有什么区别？
cover: >-
  https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1570615514153&di=6f99e51380c6212468e4565b6321a633&imgtype=0&src=http%3A%2F%2Fpic4.zhimg.com%2Fv2-38bdac71902e51febd1ab576a32c0616_1200x500.jpg
categories:
  - react
date: 2019-09-26 00:00:00
---

- a 链接实现页面跳转时整个页面会重新渲染
- link组件实现页面跳转时只会重新渲染数据发生改变的部分，`只更新变化的部分从而减少DOM性能消耗`

### 推荐阅读
- [【react-router】从Link组件和a标签的区别说起，react-router如何实现导航并优化DOM性能？](https://blog.csdn.net/sinat_17775997/article/details/66967854)
