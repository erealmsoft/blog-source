---
title: 在setState中传递对象和传递函数有什么区别？
date: 2019-09-17 00:00:00
categories:
  - react
tags:
  - 组件
  - state
cover: >-
  https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1570615514153&di=6f99e51380c6212468e4565b6321a633&imgtype=0&src=http%3A%2F%2Fpic4.zhimg.com%2Fv2-38bdac71902e51febd1ab576a32c0616_1200x500.jpg
---

### 区别

- 因为 `this.props` 和 `this.state` 可能会异步更新，所以不能在`setState`中通过传递对象方式来更新状态
- 传递对象
    - 批处理，对相同变量进行的多次处理会合并为一个，并以最后一次的处理结果为准
- 传递函数
    - 链式调用，React 会把我们更新 state 的函数加入到一个队列里面，然后，按照函数的顺序依次调用。同时，为每个函数传入 state 的前一个状态，这样，就能更合理的来更新我们的 state 了
    - 该函数有两个参数
        - prevState
        - props

### 举个栗子

```
class Test extends Component{

    state = {
        age: 0
    }

    Click1 = () => {
        this.setState({
            age: this.state.age + 1
        });

        if (true) {
            this.setState({
                age: this.state.age + 1
            });
        }
    }
    
    Click2 = () => {
        this.setState((prevState, props) => {
            return {
                age: prevState.age + 1
            }
        });

        if (true) {
            this.setState((prevState, props) => {
                return {
                    age: prevState.age + 1
                }
            });
        }
    }

    render() {
        return (
            <View>
                <button onClick={() => {this.Click1}}>pass in an object</button>
                <button onClick={() => {this.Click2}}>pass in a function</button>
                <p>age: {this.state.age}</p>
            </View>
        );
    }
}
```
- 当点击pass in an object时age的结果为1
- 当点击pass in a function时age的结果为2