---
title: 如何给组件添加默认props
date: 2019-09-24 00:00:00
categories:
  - react
tags:
  - props
cover: >-
  https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1570615514153&di=6f99e51380c6212468e4565b6321a633&imgtype=0&src=http%3A%2F%2Fpic4.zhimg.com%2Fv2-38bdac71902e51febd1ab576a32c0616_1200x500.jpg
---

### `defaultProps` 的作用：

- `defaultProps` 可以为 `Class` 组件添加默认 `props`
- 这一般用于 `props` 未赋值，但又不能为 `null` 的情况

### 添加 `defaultProps` 的两种方法

1. 在类中声明静态属性 `static defaultProps` ，这种方法只有浏览器编译以后才会生效。

    ```
    static defaultProps = {
        age: 18
    }
    
    render(){
        return(
            <h1>Hello, {this.props.name}. and  my age is {this.props.age}</h1>
        )
    }

    ```

2. 在类外为类追加 `defaultProps` 属性，这种方式会一直生效。
    ```
    class App extends Component {
        render() {
            return (
                <div>
                    {this.props.name}
                </div>
            );
        } 
    }
    App.defaultProps={
        name:"jack"
    }
    ```

### 推荐阅读
- [React 官方文档](https://zh-hans.reactjs.org/docs/react-component.html#defaultprops)