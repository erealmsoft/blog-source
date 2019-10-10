---
title: Express中Route的配置及参数传递
tags:
  - 路由
  - 参数
  - 设置
  - express
categories:
  - others
date: 2014-11-03 00:00:00
---

　　在开发公司HomeSite网站（*官网：[www.erealm.cn](http://www.erealm.cn)*）时，采用的是最近流行的全Javascript的web开发架构MEAN，分别代表的是(M)ongoDB——使用JSON风格来存储数据，使用JS来进行sql查询；(E)xpress——基于Node的Web开发框架；(A)agular——JS的前端开发框架；(N)ode.js——基于V8的运行时环境。
    
　　在处理后端逻辑时，用到了基于Node.js的MVC开发框架express，而express又有着其特有的语法特性。本文就在开发HomeSite过程中用到的express中关于route的配置进行基本的语法讲解，旨在为开发的过程做一个梳理和总结。

### 路由的配置

- 在express框架中，根目录下的app.js文件时程序的入口文件，当用户在浏览器输入网址后，程序会执行app.js文件来对程序进行模板引擎设置，路由设置和监听程序端口等。因为在该程序中有大量的路由来实现界面跳转和请求数据，将这些路由都写在app.js文件中未免显得太冗余不好维护，因此将所有的路由写在一个专门的路由配置文件routes.js中。在app.js中用express提供的require函数，取得routes.js文件的模块导出对象，并将变量app作为参数传递给该对象，从而实现了路由的功能。
　　
```javascript
    var cluster = require('cluster'),
        express = require('express'),
        hbs = require('express-hbs'),
        config = require('./config'),
        app = express(),
        expressValidator = require('express-validator');

    require('./app/routes')(app, express);
```

- 在routes.js中，`app.get()`方法是根据HTTP的get协议而将请求的不同URL路由到不同的操作。在HomeSite程序中，app.get()方法主要有两种用法：

    1. **根据URL通过回调函数路由到相应的模板引擎。**

        - 例如，若用户在地址栏输入www.erealm.cn/contact,则会根据url中的contact关键字调用回调函数`function(req,res){res.render('contact');}`,通过回调函数中的res.render()方法路由到contact.hbs页面。
            ```javascript
            app.get('/', function(req, res) {
                res.render('index');
            });
            app.get('/contact', function(req, res) {
                res.render('contact');
            });
            app.get('/about', function(req, res) {
                res.render('about');
            });
            app.get('/blog', function(req, res) {
                res.render('blog');
            });
            app.get('/work', function(req, res) {
                res.render('work');
            });
            app.get('/projectplan', function(req, res) {
                res.render('projectPlan');
            });
            ```
    2. **根据URL去调用相应的API接口，取得相应的数据。**
        - 在about.hbs页面请求employee的数据时，根据routes.js的配置，将'/app/personnel/'+language的URL请求路由到了personnel.js接口，通过personnel.js中的readStaff方法将employee的数据取出并返回给about.hbs。
            ```javascript
             getEmployeeInfo:function(language){
                return $http.get('/app/personnel/' + language);
            }
            app.get('/app/personnel/:language', require('./api/    personnel').readStaff);

            app.get('/app/partners/:language', require('./api/partners').readPartner);

            app.get('/app/projects/:language/:projects', require('./api/projects').readProjects);
            ```
        - app.post()方法是**根据HTTP的post协议而将请求的不同URL路由到相应的API接口**。在contact.hbs页面填好message表单信息后，通过/app/message的URL，将其路由到support.js的模块导出对象，通过该对象中的sendMessage方法将message表单中数据取到并完成发送邮件的操作。
            ```javascript
            app.post('/app/message', require('./api/support').sendMessage);

            app.post('/app/projectplan', require('./api/projectplan').sendProject);
            ```
### 参数的传递

  在express中进行路由分发的过程中，常常伴随着各种参数的传递。

- 在HomeSite程序中，基于get协议的参数传递是通过字符串拼接实现的。当在中文（或英文）下访问about.hbs页面时，会将当前语言状态拼接到请求的URL后面。
    ```javascript
    getEmployeeInfo:function(language){
        return $http.get('/app/personnel/' + language);
    }
    ```
- Routes.js在对该请求URL进行转发时，是通过在URL后面添加冒号（:）和当前语言状态，来和请求URL进行匹配，倘若匹配成功，则路由到personnel.js接口，在接口中通过req.params获取传过来的参数，然后取出相应的employee信息返回到about.hbs页面。
    ```javascript
    app.get('/app/personnel/:language', require('./api/personnel').readStaff);
    var language = req.params.language;
    ```
- 基于post协议进行路由的分发时，其参数的传递不同于get协议中的字符串拼接，而是单独作为参数进行传递的。
    ```javascript
    submitMessage: function(name, email, message) {
        return $http.post('/app/message', {name: name, email:email, message: message});
    }
    ```

    上面代码在客户端post了name,email,messsage三条数据，封装为Json格式后通过URL：/app/message将参数post给后端。Routes.js在匹配到URL：:/app/message后，将其路由到support.js接口，在该接口中再通过req.body获取传过来的参数。
    ``` javascript
    var name = req.body.name,
        email = req.body.email,
        message = req.body.message;
    ```
