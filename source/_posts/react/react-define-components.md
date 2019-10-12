---
title: react定义组件时有什么规定？
categories:
  - react
tags:
  - 组件
cover: >-
  https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1570615514153&di=6f99e51380c6212468e4565b6321a633&imgtype=0&src=http%3A%2F%2Fpic4.zhimg.com%2Fv2-38bdac71902e51febd1ab576a32c0616_1200x500.jpg
date: 2019-09-10 00:00:00
---

### 规则&约定

- 组件命名必须以大写字母开头
- 制定这个规则的原因
    1. 区分内置组件和用户自定义的组件
    2. 首字母大写的组件在定义时它的type会是React.Compontent类型，而小写字母开头的组件会被视为原生的DOM标签，type为'simple'
    3. 我们写的react组件使用的都是JSX语法，需要编译后在浏览器上运行，使用JSX创建元素时，会触发组件内部的`React.cteateElement()`
        - 如果是以小写字母开头的，会被React当作HTML内置组件（比如 `<div>` 或者 `<span>` 会生成相应的字符串 `'div'` 或者 `'span'` 传递给 `React.createElement`（作为参数)），这样会无法正常解析自定义组件内部的其他标签
        - 大写字母开头的元素则对应着在 JavaScript 引入或自定义的组件，如 `<Foo />` 会编译为 `React.createElement(Foo)`

### 推荐阅读
- [官方文档1](https://zh-hans.reactjs.org/docs/components-and-props.html)
- [官方文档2](https://zh-hans.reactjs.org/docs/jsx-in-depth.html#user-defined-components-must-be-capitalized)