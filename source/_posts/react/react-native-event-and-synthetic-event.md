---
title: 了解React中的合成事件及原生事件
tags: 事件
categories:
  - react
date: 2019-09-27 00:00:00
cover: >-
  https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1570615514153&di=6f99e51380c6212468e4565b6321a633&imgtype=0&src=http%3A%2F%2Fpic4.zhimg.com%2Fv2-38bdac71902e51febd1ab576a32c0616_1200x500.jpg
---

### 先简单了解一下原生事件
- DOM事件流的三个阶段
    1. 事件捕获阶段：
        - 事件从文档的根节点出发，随着DOM树的结构向事件的目标节点流去。途中经过各个层次的DOM节点，并在各节点上触发捕获事件，直到到达事件的目标节点。捕获阶段的主要任务是建立传播路径，在冒泡阶段，事件会通过路径回溯到文档根节点。
    2. 目标阶段：
        - 当事件到达了目标节点，就进入了目标阶段，然后会逆向回流，知道传播至最外层的文档节点
    3. 冒泡阶段：
        - 事件在目标元素上触发后，并不在这个元素上终止。它会随着DOM树一层一层向上冒泡，直到到达最外层的根节点。也就是说，同一个事件会依次在目标节点的父节点，父节点的父节点…直到最外层的节点上被触发

### 为什么会有合成事件
- 如果DOM上绑定了过多的事件处理函数，整个页面响应以及内存占用可能都会受到影响。React为了避免这类DOM事件滥用，同时屏蔽底层不同浏览器之间的事件系统差异，实现了一个中间层 —— SyntheticEvent
- 合成事件时浏览器原生事件的跨浏览器包装器，兼容所有浏览器，并拥有和浏览器原生事件相同的接口

### 合成事件的原理
- React并不是将click事件直接绑定在dom上面，而是采用事件冒泡的形式冒泡到document上面，在document上监听所有支持的事件
- 当事件发生并冒泡至document处时，React将事件内容封装并交由真正的处理函数运行

### react中使用事件与原生DOM事件的区别
- React事件使用驼峰命名，而不是全部小写
- 通过JSX，要传递一个函数作为事件处理程序而不是一个字符串
- 在React中你不能通过返回false来阻止默认行为，必须明确调用preventDefault

### 推荐阅读
- [JS事件那些事儿 一次整明白](https://juejin.im/post/5c092ad36fb9a049bc4c754e#comment)
- [React Events](https://reactjs.org/docs/events.html)
- [React源码解读系列 – 事件机制](http://zhenhua-lee.github.io/react/react-event.html)
