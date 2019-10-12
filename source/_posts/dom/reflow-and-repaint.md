---
title: 浏览器中的重绘和重排是什么？
categories:
  - dom
tags:
  - 渲染
date: 2019-09-16 00:00:00
---

### 浏览器是如何被渲染的

- 浏览器下载完所有页面资源后，会解析并生成两个内部数据结构
    1. DOM树（页面层次结构）
    2. 渲染树（样式，布局）
- 当浏览器渲染完一次之后，由于内容或者样式的改变，浏览器重新计算后发现元素的几何属性发生了变化（比如`宽高发生了变化`，`位置产生了偏移`），所以需要重新构建渲染树，这个过程称为重排
- 完成重排后，浏览器会重新绘制受影响的部分到屏幕中，这个过程称为重绘

### 重排和重绘的触发条件

- 通俗点讲，页面元素的删除、添加、尺寸变化都会引起重排，页面元素的颜色，透明度等变化都会引起重绘
- 在内容改变，但并不影响元素几何属性的情况下不会触发重排，所以重排必然带来重绘，但是重绘未必带来重排
- 相比较重绘，重排更加消耗性能
- 由于重绘或者重排比较消耗性能，频繁的重绘和重排更是如此，react中的virtual dom也就应运而生了

### 推荐阅读
- [whats-the-difference-between-reflow-and-repaint](https://stackoverflow.com/questions/2549296/whats-the-difference-between-reflow-and-repaint)
- [reflows-repaints-css-performance-making-your-javascript-slow](http://www.stubbornella.org/content/2009/03/27/reflows-repaints-css-performance-making-your-javascript-slow/)
- [各个浏览器中各个css属性重绘重排情况](https://csstriggers.com/)