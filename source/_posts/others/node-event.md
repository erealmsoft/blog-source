---
title: Node.js事件解析
tags:
  - Node.js
  - 事件
  - EventEmitter
categories:
  - others
date: 2014-11-04 00:00:00
---

&emsp;&emsp;Node.js 是一个快速构建网络服务及应用的平台，它采用异步式 I/O 与事件驱动的架构设计解决传统系统开发中面临的高并发问题，而理解Node.js中的事件有助于利用Node.js构建高效的系统。

## Node.js事件

&emsp;&emsp;Node.js里面的许多对象都会分发事件，比如一个net.Server对象会在每次有新连接时分发一个事件， 一个fs.readStream对象会在文件被打开的时候发出一个事件。所有这些产生事件的对象都是 `events.EventEmitter` 的实例。`Event模块`是一个简单的事件监听器模式的实现，在nodeJs中可以通过`require('events')`引入该模块。该模块包含EventEmitter类, 提供事件绑定、触发等相关方法，Node.js的大部分模块都继承自Event模块。

&emsp;&emsp;Node.js与Web前端DOM树事件机制不同之处在于不存在冒泡、捕获等行为, 也没有`preventDefault(), stopPropagation()`等方法。Node.js 在执行的过程中会维护一个事件队列，程序在执行时进入事件循环等待下一个事件到来，每个异步式I/O请求完成后会被推送到事件队列。等到线程进入事件循环以后，才会调用事件队列中的回调函数执行相应的逻辑。

## EventEmitter

### EventEmitter介绍
&emsp;&emsp;events模块只提供了一个对象：`events.EventEmitter`。EventEmitter的核心就是事件触发与事件监听器功能的封装。EventEmitter 的每个事件由一个事件名和若干个参数组成，事件名是一个字符串，通常表达一定的语义。对于每个事件，EventEmitter支持若干个事件监听器。当事件发生时，注册到这个事件的事件监听器被依次调用，事件参数作 为回调函数参数传递。简单实例如下所示：
```javascript
var events = require('events');
var emitter = new events.EventEmitter();
//注册事件监听器1
emitter.on('someEvent', function(arg1, arg2) {
        console.log('listener1', arg1, arg2);
});
//注册事件监听器2
emitter.on('someEvent', function(arg1, arg2) {
        console.log('listener2', arg1, arg2);就是
});
//触发someEvent事件
emitter.emit('someEvent', 'erealm', 2014);
```
运行结果：

listener1 erealm 2014

listener2 erealm 2014

### EventEmitter常用API

* `EventEmitter.on(event, listener)` 为指定事件注册一个监听器，接受一个字符串 event 和一个回调函数 listener。
*   `EventEmitter.emit(event, [arg1], [arg2],[...]) `发射 event 事件，传递若干可选参数到事件监听器的参数表。
*  `EventEmitter.removeListener(event,listener)`移除指定事件的某个监听器，listener必须是该事件已经注册过的监听器。
*  `EventEmitter.removeAllListeners([event])`移除所有事件的所有监听器，如果指定event，则移除指定事件的所有监听器。

### error事件

&emsp;&emsp;EventEmitter定义了一个特殊的事件error，它包含了“错误”的语义，我们在遇到异常的时候通常会触发error 事件。当 error 事件发生时，EventEmitter 规定如果没有响应的监听器，Node.js 会把它当作异常，退出程序并打印调用栈。建议一般要给分发error事件的对象设置监听器，避免遇到错误后整个程序崩溃。

### 继承EventEmitter ####
&emsp;&emsp;在JavaScript中有多种继承方式，典型的方式是使用原型方式实现继承，也可使用util模块，如下实例所示：
```javascript
var util = require('util');
var events = require('events');
var MyClass = function() { };
//使用util的inherits方法实现继承
util.inherits(MyClass, events.EventEmitter);
MyClass.prototype.ping = function() {
    this.emit('response', 'erealm');
};
var myClass = new MyClass();
myClass.on('response', function(msg) {
    console.log(msg);
});
myClass.ping();
```
## 典型实例分析

&emsp;&emsp;由于fs模块继承EventEmitter,所以在如下所示程序代码
```javascript
fs = require('fs')
fs.readFile('/etc/hosts', 'utf8', function (err,data) {
    if (err) {
        console.log(err);
    }
    console.log('ok');
});
console.log('end')
```
&emsp;&emsp;fs.readFile的第三个参数是一个函数，我们称为回调函数。进程在执行到fs.readFile的时候，不会等待结果返回，而是直接继续执行后面的语句，直到进入事件循环。当数据库查询结果返回时，会将事件发送到事件队列，等到线程进入事件循环以后，才会调用之前的回调函数继续执行后面的逻辑。
