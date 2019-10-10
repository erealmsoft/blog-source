---
title: Node.js自定义模块与使用
tags:
  - Node.js
  - 模块
  - Module
categories:
  - others
date: 2014-11-17 00:00:00
---

&emsp;&emsp;模块是Node.js 应用程序的基本组成部分，通过模块化编程可以提高程序功能模块的可复用性，从而构建一个高类聚、低耦合的系统，方便维护与测试。

## Node.js模块

&emsp;&emsp;在Node.js中，模块分为两类：一类是Node.js提供的模块，称为核心模块；另一类是用户编写的模块，称为文件模块。

&emsp;&emsp;核心模块在Node.js源代码编译的时候被编译成二进制文件，可以require(‘模块名’)去获取；其中http、fs、net等都是node.js提供的核心模块。在Node.js进程启动时，部分核心模块就被直接加载进内存中，所以这部分核心模块引入时，文件定位和编译执行这两个步骤可以省略掉，并且在路径分析中优先判断，所以它的加载速度是最快的。

&emsp;&emsp;文件模块则是在运行时动态加载，需要完整的路径分析、文件定位、编译执行过程，速度比核心模块慢。但是在程序中经过第一次使用require方法加载模块后，Node.js对所加载的原生模块或文件模块都进行了缓存，于是在第二次使用require方法加载同样的模块时，是不会有重复开销的。

## 自定义模块

&emsp;&emsp;在Node.js 应用程序中，文件和模块是一一对应的。一个 Node.js 文件就是一个模块，这个文件可能是JavaScript 代码、JSON 或者编译过的C/C++ 扩展。
在每个模块中，module.export是模块的公开接口，便于使用require 从外部获取模块的接口。


**(1)一个模块中包含多个函数** 时，模块的定义如下
```javascript            
    //testA.js
    function functionA() {
      // ...
    }
    function functionB() {
      // ...
    }
    module.exports. functionA = functionA;
    module.exports. functionB = functionB;
```
  或者将module.exports替换为exports 如下：
```javascript
    exports. functionA = functionA;
    exports. functionB = functionB;
```
**(2)只将一个对象封装到模块中** ，格式如下：
```javascript
    // car.js
    module.exports = function() {
      // ...
    }
```
或者将module.exports替换为exports 如下：
```javascript
    function car() {
      // ...
    }
    module.exports= car;   // exports= functionA;
```
&emsp;&emsp;**module.exports 与exports的区别** ：module.exports是模块的公开接口，每个模块都会自动创建一个module对象，该对象有一个exports属性，初始值是个空对象{}.exports只是module.exports的一个辅助对象，模块最终返回module.exports给模块的调用者，而不是exports。exports所起的作用是收集属性，如果module.exports当前没有任何属性，exports会将这些属性赋给module.exports, 如果module.exports已经有一些属性，那么exports的所有属性会被忽略。


## 使用模块

&emsp;&emsp;在Node.js中使用require方法引入模块，该方法会返回一个对象，它引用的是某个给定文件中的module.exports值。例如：
```javascript
    //使用原生（核心）模块
    var http = require(‘http’);
    //使用自定义模块
    var testA = require('./ testA);//引入了当前目录下的testA.js文件
    testA. functionB();
    //......
    var Car = require('./ car);
    var car= new Car();
```

&emsp;&emsp;Node.js通过require方法可以加载的模块文件类型有三种：*.js , *.json,  *.node 。

* `* .js`是文本格式的javascript文件；
* `* .json`是json格式对象，这两者(.js && .json)加载的时候被视为javascript被动态编译和处理使用；
* `* .node`是预编译好的插件模块；

Nodejs尝试加载的优先级 js文件 > json文件 > node文件

require方法根据其传入的参数决定模块的查找方式。

* `模块以 '/' 开头`表示使用文件的绝对路径。例如，require('/home/marco/foo.js') 将加载/home/marco/foo.js 文件。
* `模块以 './' 开头`表示调用 require() 时使用相对路径。也就是说，为了保证 require('./circle') 能找到，circle.js 必须和 引用模块的js文件在同一目录。
* `模块不以 '/' 或'./' 开头`表示该模块可以是一个“核心模块”，也可是一个从 node_modules 文件夹中加载的模块。