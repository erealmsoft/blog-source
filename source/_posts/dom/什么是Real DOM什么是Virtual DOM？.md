---
title: 什么是Real DOM什么是Virtual DOM？
categories:
  - dom
tags:
  - 渲染
date: 2019-09-13 00:00:00
---

### Real DOM

- 文档对象模型（Document Object Model，简称DOM），是W3C组织推荐的处理可扩展标志语言的标准编程接口.在网页上，组织页面（或文档）的对象被组织在一个树形结构中，用来表示文档中对象的标准模型就称为DOM.
- DOM实际上是以面向对象方式描述的文档模型。DOM定义了表示和修改文档所需的对象、这些对象的行为和属性以及这些对象之间的关系。可以把DOM认为是页面上数据和结构的一个树形表示，不过页面当然可能并不是以这种树的方式具体实现。

### Virtual DOM

- 指的是对真实DOM的一种模拟。相对于直接操作真实的DOM结构，我们构建一棵虚拟的树，将各种数据和操作直接应用在这棵虚拟的树上，然后再将对虚拟的树的修改应用到真实的DOM结构上。
- Virtual DOM只是一个简单的JS对象，并且最少包含tag、props和children三个属性。不同的框架对这三个属性的命名会有点差别，但表达的意思是一致的。它们分别是标签名（tag）、属性（props）和子元素对象（children）。

### 举个栗子

```javascript
    {
        tag: "div",
        props: {},
        children: [
            "Hello World", 
            {
                tag: "ul",
                props: {},
                children: [{
                    tag: "li",
                    props: {
                        id: 1,
                        class: "li-1"
                    },
                    children: ["第", 1]
                }]
            }
        ]
    }
```
`上边的例子等同于`
```html
<div>
    Hello World
    <ul>
        <li id="1" class="li-1">
            第1
        </li>
    </ul>
</div>
```

### Real DOM 和 Virtual Dom的区别

- 如果要获取页面上dom节点的值，Real DOM需要通过get…方法来获取，而Virtual Dom可以直接在js对象上拿到值，设置值也是这个道理，所以Vitrual DOM相比于Real DOM
    - 更新更快
    - 操作简单
    - 内存消耗少
- 如果没有Vitrual DOM，元素改变所引起的浏览器的重绘/重排压力会很大，引起页面卡顿等现象，借助Virtual DOM，DOM 元素的改变可以在内存中进行比较，再结合框架的事务机制将多次比较的结果合并后一次性更新到页面，从而有效地减少页面渲染的次数
