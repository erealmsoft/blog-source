---
title: RESTful API的基本设计原则
tags:
  - RESTful
  - Design
  - API
  - Principle
categories:
  - others
date: 2014-11-17 00:00:00
---

　　RESTful API的架构，是现在比较流行的一种设计思想。它在符合互联网标准的前提下，以用户容易理解，软件开发人员易于扩展的方式来构建软件结构，正受到越来越多的公司去采用。

　　自己在学习RESTful API设计的时候，也参阅了很多前辈们的文章，站在巨人的肩膀上学习了RESTful架构后，在此谈一谈自己的感受和心得，希望能作为一个入门级的向导吧。

　　API是连接你和用户的一个桥梁。设计一个API不难，你可以根据自己的喜好，根据自己的程序逻辑定义一串符合标准的字符就可以了，用户通过该API可以取得他们想要的数据或者资源。但是，设计一个好的API很难。设计API要尽可能做到让用户见名知意，以较短的字符串表达出这个API想要提供的是什么功能；同时，在API的设计上，要为以后的扩展做好准备。

## 理解RESTful的含义
　　设计者将其定名为REST，是Representational State Transfer的缩写。要理解RESTful架构，最好的方法就是去理解Representational State Transfer这个词组到底是什么意思，它的每一个词代表了什么涵义。

### 资源(Resources)
　　REST（Representational State Transfer）省略了主语，表现层（Representational）的主语其实指的是资源（Resources）。资源就是网络上的一个实体，或者说是网络上的一个具体信息。它可以是一段文本、一张图片、一首歌曲、一种服务，总之就是一个具体的实体。你可以用一个URI（统一资源定位符）指向它，每种资源对应一个特定的URI。要获取这个资源，访问它的URI就可以，因此URI就成了每一个资源的地址或独一无二的识别符。

　　所谓"上网"，就是与互联网上一系列的"资源"互动，调用它的URI。

### 表现层（Representation）
　　"资源"是一种信息实体，它可以有多种外在表现形式。我们把"资源"具体呈现出来的形式，叫做它的"表现层"（Representation）。例如文本可以用txt来表现也可以用XML、JSON、MARKDOWN的格式来表现等。

### 状态转化(State Tranfer)
　　上网，就代表了客户端和服务器端的一个交互过程。在这个过程中就会涉及到数据和状态的改变。客户端想从服务器端得到某种服务，就需要通过使用HTTP协议。HTTP协议时无状态协议，，所有的状态都保存在服务器端。HTTP中的四个基本的动词涵盖了用户的所有操作类型。对应的四个基本操作是：GET用来获取资源，POST用来新建资源（也可以用于更新资源），PUT用来更新资源，DELETE用来删除资源。

　　**综上，URI代表一种资源（Resources），客户端和服务器间传递的是资源的表现层（Representation），再通过四个基本的HTTP动词来实现表现层的状态转化（State Transfer）。**

## HTTP动词
　　在HTTP动词中，有“四个半”重要的动词经常用到。之所以说“半个”，是因为动词“PATCH”的功能与动词“PUT”非常相似，我们完全可以用动词PUT来取代PATCH的功能。这“四个半”动词为（括号中为对应的数据库操作）：

* GET（SELECT）：从服务器端取得一个特定的资源，或者整个资源列表。
* POST（CREATE）：在服务器端创建一个新的资源。
* PUT（UPDATE）：更新服务器端的资源（客户端提供改变后的完整资源）。
* PATCH（UPDATE）：更新服务器端的资源（客户端只提供改变的属性）。
* DELETE（DELETE）：从服务器端移除某个资源。

　　除此之外，还有两个不经常用到的动词：

* HEAD：取得一个资源的元数据，如数据的哈希。
* OPTIONS：获取用户操作资源的权限信息。

　　下面是一些例子：

* GET /zoos：列出所有动物园
* POST /zoos：新建一个动物园
* GET /zoos/ID：获取某个指定动物园的信息
* PUT /zoos/ID：更新某个指定动物园的信息（提供该动物园的全部信息）
* PATCH /zoos/ID：更新某个指定动物园的信息（提供该动物园的部分信息）
* DELETE /zoos/ID：删除某个动物园
* GET /zoos/ID/animals：列出某个指定动物园的所有动物
* DELETE /zoos/ID/animals/ID：删除某个指定动物园的指定动物

## 应该注意的问题
### URI中不能包含动词
　　一个好的RESTful API，会让第三方开发者利用以上的“四个半”动词就能获取到他们想要的数据。但是，在URI的字段中**不能包含动词**。因为“资源”是一种实体，所以应该是名词，动词的语义应该用上面介绍到的HTTP的“四个半”动词来表示。

　　例如，某个URI是/posts/show/1,show是动词，这个设计就是错的。正确的写法应该是/posts/1，然后用GET方法来表示“show”的动作语义。

### 将版本号放在URI中
　　一个API是用户和服务器之间的桥梁。如果对服务器端的API作了改动，而这些改动影响到了向后兼容性的话，用户就会不满意，甚至会放弃对程序的应用。所以，为了确保API的合理进化，在用户使用旧版本的同时，应该不定期地想用户介绍新版本的API，让他们及早适应新的变化。

　　一个好的RESTful API设计应该在URL上跟踪版本信息，还有一个常用的解决方式是将版本号放在HTTP请求的头信息中。但是很多第三方开发者更乐意将版本号放在URL上，这样更加方便直观。

### URL的根入口点
　　API的根入口点越简单越好，复杂的URL看起来让人枯燥繁琐，只会让用户减少。常用的两种URL根有下面两种形式：

* https://example.org/api/v1/
* https://api.example.com/v1/

　　如果应用程序设计的很大，将来还可能会进一步扩展的话，采用第二种的形式，将api写在主域名前面；如果程序的API很简单，不会有进一步的扩展，就采用第一种形式，将api放在主域名下。

### 路径（Endpoint）
　　在RESTful架构中，每个网址代表一种资源（resource），所以网址中不能有动词，只能有名词，而且所用的名词往往与数据库的表格名对应。一般来说，数据库中的表都是同种记录的"集合"（collection），所以API中的**名词也应该使用复数**。

　　举例来说，有一个API提供动物园（zoo）的信息，还包括各种动物和雇员的信息，则它的路径应该设计成下面这样：

* https://api.example.com/v1/zoos
* https://api.example.com/v1/animals
* https://api.example.com/v1/employees

## 状态码（Status Codes）
　　服务器向用户返回的状态码和提示信息，常见的有以下一些（方括号中是该状态码对应的HTTP动词）：

* 200 OK - [GET]：服务器成功返回用户请求的数据，该操作是幂等的（Idempotent）。
* 201 CREATED - [POST/PUT/PATCH]：用户新建或修改数据成功。
* 204 NO CONTENT - [DELETE]：用户删除数据成功。
* 400 INVALID REQUEST - [POST/PUT/PATCH]：用户发出的请求有错误，服务器没有进行新建或修改数据的操作，该操作是幂等的。
* 404 NOT FOUND - [*]：用户发出的请求针对的是不存在的记录，服务器没有进行操作，该操作是幂等的。
* 500 INTERNAL SERVER ERROR - [*]：服务器内部错误，用户将无法判断发出的请求是否成功。

*参考资料：[Principles of good RESTful API Design](http://codeplanet.io/principles-good-restful-api-design/)　　　　[理解RESTful架构](http://www.ruanyifeng.com/blog/2011/09/restful.html)*