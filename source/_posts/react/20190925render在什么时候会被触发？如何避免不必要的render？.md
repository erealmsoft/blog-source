---
title: render在什么时候会被触发？如何避免不必要的render？
tags:
  - 组件
  - render
cover: >-
  https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1570615514153&di=6f99e51380c6212468e4565b6321a633&imgtype=0&src=http%3A%2F%2Fpic4.zhimg.com%2Fv2-38bdac71902e51febd1ab576a32c0616_1200x500.jpg
categories:
  - react
date: 2018-09-25 00:00:00
---

### render触发的条件
- 第一次挂载
- state改变
- props改变

### 避免不必要的render
- 利用shouldComponentUpdate钩子函数，通过它的返回值react会决定要不要render，返回false不会渲染
