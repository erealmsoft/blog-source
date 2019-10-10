---
title: 开始使用Hook吧
date: 2019-09-20 00:00:00
categories:
  - react
tags:
  - 组件
  - Hook
cover: >-
  https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1570615514153&di=6f99e51380c6212468e4565b6321a633&imgtype=0&src=http%3A%2F%2Fpic4.zhimg.com%2Fv2-38bdac71902e51febd1ab576a32c0616_1200x500.jpg
---

### Hook是什么

- Hook是React16.8的新增特性，提供内置钩子函数（也可自定义），它可以让你在不编写 class 的情况下使用 state 以及其他的 React 特性
- 在以函数声名的组件中使用，不可以在class声名的组件中使用

### 如何使用Hook（以使用state为例）

- 引用

    ```javascript
        import React, { useState } from 'react';
    ```

- 定义及使用
    - 使用useState会返回两个对象
        1. 经过初始化的state
        2. 改变state的方法

    ```
        function Example() {
            // 声明一个新的叫做 “count” 的 state 变量
            const [count, setCount] = useState(0);

            return (
                <div>
                    <p>You clicked {count} times</p>
                    <button onClick={() => setCount(count + 1)}>
                            Click me
                    </button>
                </div>
            );
        }
	```

### Hook有哪些优势呢？

1. 避免编写重复代码

    ```javascript
        componentDidMount() {
            document.title = `You clicked ${this.state.count} times`;
        }

        componentDidUpdate() {
            document.title = `You clicked ${this.state.count} times`;
        }
    ```
    ```javascript
        useEffect(() => {
            document.title = `You clicked ${count} times`;
        });
    ```

2. 将紧密性强的代码放到一起执行，逻辑就会更好理解

    ```javascript
        componentDidMount() {
            ChatAPI.subscribeToFriendStatus(
                this.props.friend.id,
                this.handleStatusChange
            );
        }

        componentWillUnmount() {
            ChatAPI.unsubscribeFromFriendStatus(
                this.props.friend.id,
                this.handleStatusChange
            );
        }

        handleStatusChange(status) {
            this.setState({
                isOnline: status.isOnline
            });
        }
    
    ```

    ```javascript
        useEffect(() => {
            function handleStatusChange(status) {
                setIsOnline(status.isOnline);
            }

            ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
            // Specify how to clean up after this effect:
            return function cleanup() {
                ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
            };
        });
    ```

    `useEffect返回的函数会在组件卸载时执行`

### 推荐阅读

- [hook文档，从一到八建议全读](https://zh-hans.reactjs.org/docs/hooks-intro.html)


        


