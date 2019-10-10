---
title: 认识一下Controlled Component 与 Uncontrolled Component
date: 2019-09-23 00:00:00
categories:
  - react
tags:
  - 组件
cover: >-
  https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1570615514153&di=6f99e51380c6212468e4565b6321a633&imgtype=0&src=http%3A%2F%2Fpic4.zhimg.com%2Fv2-38bdac71902e51febd1ab576a32c0616_1200x500.jpg
---

### 受控组件

- React的state为唯一数据源，并且每个state突变都有一个相关的处理函数，这使得修改或验证用户输入变得简单。

``` javascript
class NameForm extends React.Component {
    constructor(props) {
    super(props);
    this.state = {value: ''};

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
    }

    handleChange(event) {
    this.setState({value: event.target.value});
    }

    handleSubmit(event) {
    alert('提交的名字: ' + this.state.value);
    event.preventDefault();
    }

    render() {
    return (
        <form onSubmit={this.handleSubmit}>
        <label>
            名字:
            <input type="text" value={this.state.value} onChange={this.handleChange} />
        </label>
        <input type="submit" value="提交" />
        </form>
    );
    }
}
```

### 非受控组件

- 将真实数据存储在DOM节点中，所以在使用非受控组件时，有时候反而更容易同时集成React和非React代码

``` javascript
class NameForm extends React.Component {
    constructor(props) {
    super(props);
    this.handleSubmit = this.handleSubmit.bind(this);
    this.input = React.createRef();
    }

    handleSubmit(event) {
    alert('A name was submitted: ' + this.input.current.value);
    event.preventDefault();
    }

    render() {
    return (
        <form onSubmit={this.handleSubmit}>
        <label>
            Name:
            <input type="text" ref={this.input} />
        </label>
        <input type="submit" value="Submit" />
        </form>
    );
    }
}
```

### 推荐阅读
- [受控组件(Controlled Components)和不受控组件](https://segmentfault.com/a/1190000011004617)
- [controlled components](https://reactjs.org/docs/forms.html#controlled-components)
- [stack over flow](https://stackoverflow.com/questions/42522515/what-are-controlled-components-and-uncontrolled-components)

