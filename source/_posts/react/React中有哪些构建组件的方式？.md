---
title: React中有哪些构建组件的方式？
categories:
  - react
tags:
  - 组件
cover: >-
  https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1570615514153&di=6f99e51380c6212468e4565b6321a633&imgtype=0&src=http%3A%2F%2Fpic4.zhimg.com%2Fv2-38bdac71902e51febd1ab576a32c0616_1200x500.jpg
date: 2019-09-11 00:00:00
---

### React中有哪些构建组件的方式

1. 函数定义的无状态组件
    - 语法：
        ``` javascript
		function Component(props, /* context */) {
		          return <div>Hello {props.name}</div>
		      }
		ReactDOM.render(<Component name="Jack" />, mountNode)
		```
    - 特点：
        - 组件不会实例化，无法访问到组件内的this对象，但整体渲染性能提升
		- 无法访问生命周期方法，不能参与各个生命周期的管理
        - 无状态，所以不涉及state的操作，只能根据传入的props进行展示

2. es6形式的React.Component定义的组件
    - 语法：
        ``` javascript
		class Component extends React.Component{
		            constructor(props){
		                super(props);
		            }
		            
		            handleClick(){
		                console.log('hello world');
		            }
		            
		            redner(){
		                return(
		                    <div onClick={() => {this.handleClick()}}>React Component</div>
		                )
		            }
	     }
		```
    - 特点：
        - 有状态，会被实例化，可以访问组件生命周期
        - 成员函数不会自动绑定this，需要开发者手动绑定，否则this不能获取到当前组件实例对象

3. es5原生方式React.createClass定义组件
    - 语法：
        ``` javascript
		var Component = React.createClass({
		            render: function(){
		                <div>React Component</div>
		            }
		})
		```
    - 特点：
        - 有状态，会被实例化，可以访问组件生命周期
		- 会自动绑定this，导致不必要的性能开销

### 它们的区别



### 这几种构建方法的区别

|             | React.createClass | Function                       | Class       |
| ----------- | ----------------- | ------------------------------ | ----------- |
| State       | Yes               | No                             | Yes         |
| Life Cycle  | Yes               | No                             | Yes         |
| This        | Auto Bind         | Can't access this: no instance | Manual Bind |
| Performance | Low               | Hight(stateless)               | Low         |
| Status      | Deprecated?       | In Use                         | In Use      |





