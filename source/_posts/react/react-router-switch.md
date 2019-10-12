---
title: 为什么React Router v4中使用 switch 关键字
tags:
  - switch
cover: >-
  https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1570615514153&di=6f99e51380c6212468e4565b6321a633&imgtype=0&src=http%3A%2F%2Fpic4.zhimg.com%2Fv2-38bdac71902e51febd1ab576a32c0616_1200x500.jpg
categories:
  - react
date: 2019-09-26 00:00:00
---

- 由于router和switch对于路由的渲染策略不同，对router来说，如果有的链接既可以被路由A匹配，又可以被路由B匹配，那么Router会同时渲染它们
- 对于switch来说，它只会渲染符合条件的第一个路径，避免重复匹配
