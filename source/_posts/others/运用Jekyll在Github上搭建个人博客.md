---
title: 运用Jekyll在Github上搭建个人博客
tags:
  - Jekyll
  - Github
  - Github Pages
  - blog
  - 博客
  - markdown
  - ruby
  - rubyrem
  - author
  - site
  - page
categories:
  - others
date: 2014-11-17 00:00:00
---

&emsp;&emsp;2010年开始，有一些程序员开始在`github`网站上搭建 `blog` 。因为github提供无限流量，免费各地访问速度都比较理想，他们对`blog`拥有绝对管理权，这样不管何时何地，只要向主机提交 `commit` ，就能发布新文章。   

&emsp;&emsp;我们的网站博客就借鉴了这一技术，下面我简单介绍一下如何用`jekyll`集成`github`搭建个人博客。   
                           
## Github Pages
&emsp;&emsp;`Github`是现在最流行的代码仓库，有时候为使项目更方便的被人理解，项目必须要有介绍页面。`Github` 就提供了`Github Pages`的服务，不仅可以方便的为项目建立介绍站点，也可以用来建立个人博客。  
&emsp;&emsp;`Github Pages` 是一个具有版本管理功能的代码仓库，每个项目都有一个主页，列出项目的源文件。以下为我们网站博客`Github Pages`的源文件：

&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;![](http://i.imgur.com/lgb52YE.png)  

&emsp;&emsp;Pages功能，允许用户自定义项目首页，用来替代默认的源码列表。所以，`Github Pages` 可以被认为是用户编写的、托管在`github` 上的静态网页。它允许站内生成网页，但也允许用户自己编写网页上传，但上传网页必须经过`Jekyll` 程序处理。  
&emsp;&emsp;`Github Pages` 有以下几个优点：  
&emsp;&emsp;&emsp;&emsp;- 使用标记语言，比如`Markdown`    
&emsp;&emsp;&emsp;&emsp;- 轻量级的博客系统，没有麻烦的配置   
&emsp;&emsp;&emsp;&emsp;- 无需自己搭建服务器   
&emsp;&emsp;&emsp;&emsp;- 根据`Github` 的限制，对应的每个站有300MB空间   
&emsp;&emsp;&emsp;&emsp;- 可以绑定自己的域名   

## 建立Github Pages
&emsp;&emsp;我在这里用到了`Github` 提供的`Github pages generator` 的功能，减少了使用的命令数量，也绕开了远程代码库这个概念。通过`SSH Keys` 配置好`github` 之后，在`github.com` 上创建代码库。`GitHub Pages` 分两种，一种是你的`GitHub` 用户名建立的`username.github.io` 这样的用户&组织页（站），另一种是依附项目的`pages` 。而我们网站博客采用的是第一种，登录到自己的`Github` 账户，选择“`New repository` ”，新建一个名为`erealm.github.io` 的代码库，每个用户名下面只能建立一个。创建之后点击`Admin` 进入项目管理，可以看到是这样的界面：   
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;![](http://i.imgur.com/5Ty6vOn.png)   
&emsp;&emsp;因为我们网站的二级域名免费，所以在`erealm` 的二级域名下添加一条A记录，地址就是`Github Pages` 的服务`IP` 地址：`207.97.227.245` 。  
&emsp;&emsp;建立好代码库之后，提交一个`index.html` 文件，然后`push` 到`GitHub` 的`master` 分支（也就是普通意义上的主干）。第一次页面生效需要一些时间，大概10分钟左右。生效之后，访问`erealm.github.io` 就可以看到我们上传的页面了，erealm.github.com就是我们的博客。如果我们需要通过自己的域名来访问，需要在项目的根目录下新建一个名为CNAME的文件，文件内容为：[blog.erealm.cn](http://blog.erealm.cn/ "blog.erealm.cn")即可。

## Jekyll模版系统
&emsp;&emsp;`Jekyll（发音/'dʒiːk əl/，"杰克尔"）` 是一个简洁的、特别针对博客平台的静态站点生成器，它会根据网页源码生成静态文件。它使用一个模板目录作为网站布局的基础框架，并在其上运行 `Textile 、 Markdown 或 Liquid`  标记语言的转换器，最终生成一个完整的静态Web站点，可以被放置在任何Web服务器上。它同时也是` GitHub Pages` ，在后台所运行的引擎。   
&emsp;&emsp;` Jekyll` 完全推翻了传统网站的维护方式，它直接回到了“原点”——作者只需要维护文本文件，每一篇日志就是一个文件，程序会根据模板设置自动把这些文本文件翻译为网页。这些文本文件不用HTML，而是用简化版本的`Markdown（MD）` 或者其它可最终翻译为`HTML` 的伪标记语言。   
&emsp;&emsp;对于个人博客，`Jekyll` 有几个明显的优势：   
&emsp;&emsp;-快速访问和弱服务器需求  
&emsp;&emsp;-高安全性   
&emsp;&emsp;-版本控制   
&emsp;&emsp;-简单部署   
&emsp;&emsp;-文本编辑器和自由格式书写          
      
### 1.安装      
      
&emsp;&emsp;我们将之前建立的代码库`clone` 下来至前端开发神器`Webstorm` 里。因为`Jekyll` 使用动态脚本语言[ Ruby ](http://zh.wikipedia.org/wiki/Ruby "Ruby")写成。所以首先我们需先下载并安装[Ruby(中文)](https://www.ruby-lang.org/zh_cn/downloads/ "Ruby(中文)")。   
   
&emsp;&emsp;安装`Jekyll的` 最好方式是通过`RubyGems` ，所以我们在`Webstorm` 终端里输入：    
```bash
    $ gem install jekyll    
```
&emsp;&emsp;`Jekyll` 依赖以下的`gems` 模块： `liquid 、 fast-stemmer 、 classifier 、 directory_watcher 、 syntax 、 maruku 、 kramdown 、 posix-spawn 和 albino `。它们会被`gem install`命令自动安装。如果你在`gem`的安装过程中遇到了问题，你可能需要安装用于在`Ruby 1.8` 上编译扩展模块的头文件。  
我们在安装时`Windows` 平台上看到如下错误提示信息： `Failed to build gem native extension`  ，则需要安装 [RubyInstaller Devkit](https://github.com/oneclick/rubyinstaller/wiki/development-kit "RubyInstaller Devkit")。  

### 2. 使用         
      
#### (1)Jekyll博客站点搭建步骤      
      
&emsp;&emsp;一旦`Jekyll` 安装成功后，搭建一个`Jekyll` 博客站点通常包括下面几步：   
&emsp;&emsp;&emsp;&emsp;1.设定站点的基本结构，使用`HTML和Liquid` 模板语言创建网页布局;   
&emsp;&emsp;&emsp;&emsp;2.创建一些帖子，或者从以前的博客平台导入;   
&emsp;&emsp;&emsp;&emsp;3.在本地测试站点，查看效果;   
&emsp;&emsp;&emsp;&emsp;4.部署网站;    
     
&emsp;&emsp;`Jekyll` 从核心上来说是一个文本转换引擎。该系统内部的工作原理是：输入一些用自己喜爱的标记语言格式书写的文本，可以是`Markdown、Textile或纯粹的HTML` ，它将这些文本混合后放入一个或一整套页面布局当中。  
我们的的`Jekyll` 博客站点通常具有如下结构：   
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;![](http://i.imgur.com/YnvhCXA.jpg)   

#### (2)各个文件夹及文件作用  
`_config.yml` 文件   
配置文件，用来定义想要的效果；

`_includes/`    
该目录存放可以与`_layouts和_posts` 混合、匹配并重用的文件。

`_layouts/`   
该目录存放用来插入帖子的网页布局模板。页面布局基于类似博客平台的“一个帖子接一个帖子”的原则，通过YAML前置数据定义。`Liquid` 标签用于在页面上插入帖子的文本内容。

`_posts/`    
该目录下存放的可以说成是你的“动态内容”。这些文件的格式很重要，它们的命名模式必须遵循 `YEAR-MONTH-DATE-title.MARKUP`  。每一个帖子的固定链接`URL` 可以作弹性的调整，但帖子的发布日期和转换所使用的标记语言会根据且仅根据文件名中的相应部分来识别。

`_site`     
这个是`Jekyll` 生成的最终的文档   
   
`index.html和其他HTML/Markdown/Textile文件`     
如果一个文件的头部存在YAML前置数据的部分，那么`Jekyll` 将会自动处理转换该文件并传送到站点路径下。这对于站点的根目录或其他任意子目录下的所有` .html 、 .markdown 、 .textile ` 文件都适用。

`其他文件/目录`         
除了以上提到的文件之外，每一个其他的、不以下划线_开头的目录和文件都会被照原样传送到站点路径下。    
下图为网站博客中个目录及文件：   
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;![](http://i.imgur.com/d4AAKU7.png)         

### 3.Jekyll的配置   
&emsp;&emsp;博客中配置文件`_config.yml` 内容如下：   
```yml
    paginate: 10 # pagination based on number of posts   
    paginate_path: "page:num"   
    highlighter: true   
    markdown: kramdown   

    defaults:
     -
    scope:
      path: "" # empty string for all files
    values:
      title: eRealm Info & Tech

    description: eRealm Info & Tech
    author:
      name: erealm
      email: hello@erealm.cn
      github: erealm
      weibo: erealm2014
      bio: SOLVING YOUR PROBLEMS BY MAKING YOUR OWN SOFTWARE!
      email_md5: d7500acdff95da1b6a98acac373cae8b
    writer:
      don:
        display_name: 薛栋
        gravatar: 594296827ff9539ded708e45ec92d528
        email: xuedong369@gmail.com
      emma:
        display_name: 李晋
        gravatar: af6bee6db31ae79eee100c5031156561
        email: emma@erealm.cn
      guo:
        display_name: 郭建刚
        gravatar: 1a8482e680b0ccd153b724e831956562
        email: hoveagle@gmail.com
      zhang:
        display_name: 张加帅
        gravatar: c715af96177682bd359e307742016f24
        email: jiashuai1215@gmail.com
      dang:
        display_name: 党建
        gravatar: 396f98e19be58c81f25060b4108595bd
        email: hunterdang@gmail.com
      erealm:
        display_name: 瑞木
        gravatar: d7500acdff95da1b6a98acac373cae8b
        email: hello@erealm.cn
    rss_path: feed.xml
    categories_path: categories.html
    tags_path: tags.html

    BASE_PATH:  
```
&emsp;&emsp;分别配置了博客的`分页功能、高亮显示和Markdown` 标记语言转换引擎。   
&emsp;&emsp;主页中用以下代码实现文章分页： 
```  
    {% for post in paginator.posts %}
        <a href="{{ post.url }}">{{ post.title }}</a>
    {% endfor %} 
```   
&emsp;&emsp;设定`kramdown为Markdown`标记语言转换引擎。也可以使用 `RDiscount 取代 kramdown` 作为你的`Markdown` 标记语言转换引擎，只需确认安装：
```bash
    $ gem install rdiscount
```
&emsp;&emsp;并通过以下命令行参数执行`Jekyll` ：
```bash
    $ jekyll --rdiscount
```
&emsp;&emsp;或者也可以在你站点下的 `_config.yml`  文件中markdown的参数变为`rdiscount` 。

### 4.YAML Front Matter和模板变量

&emsp;&emsp;对于使用`YAML` 定义格式的文章，`Jekyll` 会特别对待，他的格式要求比较严格，例如博客文章中：
```
    ---
    layout: post
    title: 初涉Grunt心得
    author: don
    categories: [home]
    tags: [Grunt,自动化,package,gruntfile,压缩,合并,配置,插件]
    fullview: false
    ---
```
&emsp;&emsp;前后的---不能省略，在这之间，可以定一些需要的变量，`layout` 就是调用`_layouts` 下面的某一个模板，他还有一些其他的变量可以使用：   
&emsp;&emsp;permalink：可以对某一篇文章使用通用设置之外的永久链接   
&emsp;&emsp;published：可以单独设置某一篇文章是否需要发布   
&emsp;&emsp;category：设置文章的分类   
&emsp;&emsp;tags：设置文章的`tag `    
&emsp;&emsp;上面的`title` 就是自定义的内容，你也可以设置其他的内容，在文章中可以通过`{{ page.title }}` 这样的形式调用。   
   
### 5.博客文章作者及头像的添加       

#### (1)Jekyll模板全局变量      

`site` :`全站的信息` +`_config.yml` 文件中的配置选项;   
`page` :这个变量中包含`YAML` 前置数据,另外加上两个额外的变量值:`url和content` ;   
`content` :在布局模板文件中，这里变量包含了页面的子视图。这个变量将会把渲染后的内容插入到模板文件中。这个变量不能在文章和页面文件中使用;   
`paginator` :一旦`paginate` 配置选项被设置了，这个变量才能被使用;       

#### (2)Jekyll模板Site变量   
`site.time` :当前的时间(当你运行`Jekyll` 时的时间);   
`site.posts` :一个按时间逆序的文章列表;    
 
`site.related_posts` :如果当前被处理的页面是一个文章文件，那这个变量是一个包含了最多10篇相关文章的列表。默认来说，这些相关文章是低质量但计算快的。为了得到高质量但计算慢的结果，运行`Jekyll` 命令时可以加上`--lsi` 选项。(潜在语意索引)   

`site.categories.CATEGORY` :所有在`CATEGORY` 分类中的文章列表   
`site.tags.TAG` :所有拥有`TAG` 标签的文章的列表   

`site.[CONFIGURATION_DATA]` :截止0.5.2版本，所有在`_config.yml` 中的数据都能够通过site变量调用。举例来说，如果你有一个这样的选项在你的配置文件中:`url: http://higrid.net` ，那在文章和页面文件中可以这样调用`{ { site.url } }` 。`Jekyll` 并不会自动解析修改过的`_config.yml` 文件，你想要启用新的设置选项，你需要重启`Jekyll`        
        
#### (3)Jekyll模板Page变量           
     
`page.content`:页面中未渲染的内容   
`page.title`:文章的标题    
`page.url`:除去域名以外的URL 
`page.date`:指定每一篇文章的时间，这个选项能够覆盖一篇文章中前置数据设置的时间，它的格式是这样的:YYYY-MM-DD HH:MM:SS   
`page.id`:每一篇文章的唯一标示符(在RSS中非常有用)  
`page.categories`:这篇文章隶属的分类的一个列表，分类是通过在_post目录中的目录结构推导而来的。这个变量也能在YAML前置数据中被指定    
`page.tags`:这篇文章的标签的列表。这些数据能够在YAML前置数据中指定   
`page.next`:按时间序的下一篇文章   
`page.content`:按时间序的上一篇文章             
        
#### (4)Jekyll模板Paginator变量          
      
`paginator.per_page`:每一个页面上文章的数量   
`paginator.posts`:当前页面上可用的文章   
`paginator.total_posts`:所有文章的数量   
`paginator.total_pages`:所有页面的数量   
`paginator.page`:当前页面的数量   
`paginator.previous_page`:前面的页面的数量   
`paginator.next_page`:接下来的的页面的数量          
        
#### (5)作者名及头像加载          
      
&emsp;&emsp;我们在网站博客`_config.yml` 文件中写入如下等文章作者代码：
```yml    
    writer:   
          don:   
            display_name: 薛栋   
            gravatar: 594296827ff9539ded708e45ec92d528   
            email: xuedong369@gmail.com   
```
&emsp;&emsp;通过向主页以及每个文章模版里最开始加入以下`Liquid` 代码：

    {% assign author = site.writer[post.author] %}
 
&emsp;&emsp;我们将文章最开始---内`YAML` 中的作者名和`_config.yml` 中全局的`writer` 里的`author` 名对应并赋给全局变量`author` 。
&emsp;&emsp;主页中我们使用如下代码进行调用对应`author` 中的`display_name` 和头像属性：   
```  
    <img alt="{{ author.display_name }}" src="http://www.gravatar.com/avatar/{{ author.gravatar }}?s=40">
```
&emsp;&emsp;其中[gravatar](http://en.gravatar.com/ "gravatar")为第三方头像存储网站，它能针对每个头像生成唯一的`ID`。   

&emsp;&emsp;现在本地环境就基本搭建完成了，进入之前我们建立的博客目录，运行下面的命令：```bash
    $ jekyll serve   
``` 
&emsp;&emsp;这个时候，你就可以通过`localhost:4000` 来访问了。      
&emsp;&emsp;以上为个人学习`Jekyll在github` 搭建静态个人博客总结经验，初次学习，如有错误还望指出~
