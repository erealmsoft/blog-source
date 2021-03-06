---
title: 我们为什么要开发一个开源的企业网站？
tags:
  - web
  - 开源
  - node.js
categories:
  - others
date: 2014-11-02 00:00:00
---

### 前言
- 今年七月份，我和几个小伙伴们合伙建立了一个开发团队，取名为`西安瑞木信息技术有限公司`，英文名是`eRealm`。团队专注于Web开发，并提供Web开发的咨询及架构搭建。业务开展如火如荼的同时，团队宣传就提上了日程，作为正规军总不能没有宣传阵地吧。所以迫切需要搭建公司网站出来。

- 确定目标后我们就开始考虑如果构建一个公司企业网站。先是进行业内调查，看了看别人家的公司网站是怎么做的。总体来讲，国外网站的设计和使用的技术总能比国内高很大一截，国内很多公司，甚至是很多软件公司都不注重公司网站的构建，网站千篇一律，没有特色。很多公司网站都是使用Wordpress，然后自定义皮肤。也有一些设计类公司，网站页面做的很漂亮，设计也前卫，但是前端源代码写的一塌糊涂。我们起初的方案也是想使用Wordpress作为基础来设计公司网站，网站UI从已有开源的皮肤基础上修改。这样既能节省开发成本，又能体现独一无二。其实，刚开始也是这么做的，并且已经做出来了第一版了。只是实在是觉得和别人家的网站差别不大，太普通了，并且网站也没有任何体现我们专注于Web开发这一特质。权衡再三之后，决定从头开发一个企业网站出来，使用我们团队擅长的技术重新开发一个网站出来。决定前端使用`AngularJS`和`Bootstrap`构建，后端使用`node.js`和`Express`构建。经过一个多月的努力，我们的技术团队利用工作之余的时间终于完成的项目的第一版。下面将详细介绍这个项目的基础结构。*

### 项目整体介绍
- 技术上，项目前端使用`AngularJS`和`Bootstrap`，后端使用`node.js`和`Express`。网站自动化构建工具使用`grunt`。网站整体应用了流行扁平化设计和响应式设计。当然，UI设计是我们团队的弱项，所以很多都是借鉴（~~抄袭~~）了别人的设计。网站前端代码基于`HTML5`，支持Chrome、Safari、Firefox及IE9+，使用IE8浏览器打开网站会自动跳转到引导用户下载现代浏览器的页面中。网站应用了`响应式设计`，所以在智能手机上也可以愉快地浏览。

- 项目是完全开源的，`github`上的地址是[eRealm](https://github.com/erealm/HomeSite)，项目演示地址，也是我们公司的主页[eRealm Info & Tech](http://www.erealm.cn)。

### 代码结构介绍
- 推荐使用`Webstorm`打开项目。打开项目后，代码结构如下图所示：

![Imgur](http://i.imgur.com/SjV97nF.png)

- 在主体结构中从上到下介绍。`app`文件夹包含了所有后端代码；`build`文件夹中包含了最新数据库备份；`config`包含有网站整体的配置；`logs`文件夹包含网站后端记录的日志文件；`node_modules`是包含所有的`node.js`依赖包（源代码中初始没有此文件夹，运行`npm install`命令后所有加载的依赖包放置在此文件夹中）；`public`文件夹包含了所有的前端代码，包括JavaScript、less、图片、Webfont等；`.bowerrc`中定义了[`bower`](http://bower.io/)管理前端库的下载地址；`bower.json`则配置了项目需要的前端库；`.jshintre-client`和`.jshintrc-server`分别为前后端JavaScript代码规范检查规则；`.travis.yml`为[travis]（https://travis-ci.org/）自动编译配置；`app.js`为node.js启动脚本文件；`build.sh`为单独编写的自动发布bash命令；gruntfile.js为[`grunt`](http://gruntjs.com)配置文件；newrelic.js为[`newrelic`](http://newrelic.com)的配置文件，用于监控网站性能；`package.json`包含了所有node.js依赖包配置。

### 项目后端结构介绍
- 项目后端代码架构如下图所示：

![Imgur](http://i.imgur.com/PMMGvUy.png)

- 主要分为两大部分：`app`和`config`。`app`里面按照职责不同来分类，每个脚本文件对应于不同的模块；`api`文件夹包含了所有api对应的业务逻辑代码，`helper`放置一些公用方法，如邮件发送、日志记录、数据库连接等等；`templates`放置的是静态邮件模板；`views`是后端页面模板，使用了`handlebar`模板引擎，其中`http`中放置系统错误显示页面，`layouts`放置模板页；`routes`是`express`对应的路由配置，所有的页面和API的路由配置都在这个文件中。`config`文件夹中为系统配置，按照不同环境分为开发和现场两个环境配置，`all.js`放置共通配置，`development.js`放置开发环境对应配置而`production.js`放置线上环境配置。配置内容包括邮件发送、数据库连接及一些第三方API所需的key等等。

### 项目前端结构介绍
- 项目前端代码结构如下所示：

![Imgur](http://i.imgur.com/4WEeYLg.png)

- 前端代码全部放置于`public`文件夹下。`data`目录包含一些静态json格式数据，后期可能会考虑放到数据库中。`helper`中是浏览器下载引导页面；`images`包含了所有项目中用到的图片，我们尽量使用第三方的图片服务器保存图片，一些小图标也尽量使用webfont。`JavaScripts`文件夹包含所有JavaScript文件，其中`app`子目录放置业务代码，业务代码都是按照业务不同封装成了不同的`angularjs` controller；`debug`子目录放置调试用代码，而`libs`方式前端JavaScript库，项目中使用得JavaScript库有`angularjs`、`jQuery`及一些插件；`clients.js`是所有ajax请求函数；`erealm.js`是angularjs的主模块；`language.js`包含了所有多语言配置，目前支持中英文。`stylesheets`包含了所有的css样式及webfont，除了第三方库之外，自定义的样式全部使用了`less`。作为一种惯例，项目中添加了`humans.txt`文件，表明项目的作者信息。有关humans.txt，可以参考官方网站[humans.txt](http://humanstxt.org)。

### 自动化构建工具介绍
- 项目自动化构建使用`grunt`。grunt的使用涉及开发、调试、发布阶段。开发阶段使用了图片压缩和前端代码格式美化，使用的工具是`imagemin`和`jsbeautifier`，运行`grunt prepare`命令。调试阶段使用了代码规范检查、less编译、自动添加浏览器前缀、自动加载运行nodejs并打开浏览器、实时监控代码变化并刷新页面等。开发中，使用`grunt`命令即可，为默认grunt命令。发布阶段包含了JavaScript及css合并压缩，并在文件路径上添加哈希值来避免浏览器缓存问题，同时删除开发环境中使用的代码，使用`grunt build`命令即可把代码切换为发布环境。

- 具体的使用grunt方法及相关工具的介绍，后期会有专门的技术文章讲解，这里不会详细设计技术细节。

### 后期持续的改进点
- 项目完成的比较仓促，但是我们尽量保持代码的整洁和可维护性，一些编码方式也借鉴当前流行的最佳实践。但理想是美好的，现实总是不会做到那么完美，需要不断的完善。目前存在的问题是后端代码结构不够清晰、整体代码中无用代码还没有来得及移除。框架上期望把`jQuery`去掉，只使用`Angularjs`，目前只做到了尽量不用`jQuery`中的方法。小图标的使用上`Bootstrap`和
`Font Awesome`重复，后期会逐步删除`Font Awesome`而只使用`Bootstrap`中带的小图标。目前，最大的问题是项目没有完整的自动化测试，这个后期会逐步添加。

### 总结
- 以上是这个开源项目的整体技术结构介绍。在这个项目中，我们会持续使用最流行的Web技术，希望得到大家的持续关注，如果有开发者能一块贡献一些代码，我们将会非常高兴。我们已经在github.io上构建了一个技术平台来发布Web技术文章，网址是blog.erealm.cn。博客网址也同样开源，使用了[`Jekyll`](http://jekyllrb.com/)构建。`Jekyll`非常强大，最大的特点是使用markdown格式来发布文章。博客的代码在这里：[github](https://github.com/erealm/erealm.github.io)。

- 我们做这个开源的项目的目的有两个，其一是通过这个项目来展示我们做Web项目的实力，及培养团队技术水平。其二是借助这个项目，能和同行们有个技术上的互动和交流。如果我们的项目能让一些新手们学到一些做Web项目的经验，我们就很知足了。技术是不断革新的，而国内Web技术向来是落后于国外好几年，这个是不争的事实。我们erealm团队乐意为国内Web贡献自己的力量，也欢迎国内同行们和我们交流Web开发经验。
