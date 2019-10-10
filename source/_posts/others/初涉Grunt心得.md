---
title: 初涉Grunt心得
tags:
  - Grunt
  - 自动化
  - package
  - gruntfile
  - 压缩
  - 合并
  - 配置
  - 插件
categories:
  - others
date: 2014-11-04 00:00:00
---

&emsp;&emsp;网站的建立让我逐步学习到以前从未接触过的技术，这里就简单谈谈网站构建时`Grunt`自动化工具的使用心得。随着网站的开发进行，慢慢认识到`Grunt`就是一个能在开发中精简流程、提高效率、减少错误率的自动化工具。它能有效的简化庞大复杂系统的维护、打包、发布等流程，从而节省时间。

&emsp;&emsp;`Grunt`一个基于`Node.js`的命令行的前端 `Javascript` 自动化构建工具。是帮助开发者完成大部分重复性工作的有效工具。例如：    
 &emsp;&emsp;- 压缩文件   
 &emsp;&emsp;- 合并文件   
 &emsp;&emsp;- 简单语法检查   
&emsp;&emsp;`npm`是 `Node.js` 的包管理工具，而`Grunt`和`grunt插件` 是基于`npm` 安装并管理的。Grunt 0.4.x 版本必须配合Node.js 0.8.0以上的版本使用。

### 安装CLI
&emsp;&emsp;因为 `grunt` 是基于 `Node.js` 的，所以我们需要安装 `Node.js` 环境，在 `WebStorm` 的 `Terminal` 命令行中运行 `npm install -g grunt-cli` 将 `Grunt` 命令行安装到全局环境中。此时， `Grunt` 命令就被加入到系统路径中了，以后就可以在任何目录下执行此命令了。

&emsp;&emsp; `Grunt CLI` 的任务是调用与 `Gruntfile` 在同一目录中 `Grunt`,所以安装了 `grunt-cli` 并不等于安装了 `Grunt` 。网站中运行 `grunt` 时它会利用 `node` 提供的 `require()` 系统查找本地安装的 `Grunt`。所以可以在项目的任意子目录中运行grunt。如果找到本地安装的 `Grunt`， `CLI` 就将其加载，并传递 `Gruntfile` 中的配置信息，然后执行所指定的任务。图为网站中 `Gruntfile.js` 文件。   
 ![图 1](http://i.imgur.com/giy5QsM.jpg%22%E5%9B%BE1%22)   
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;`图 1`
         
### 安装Grunt
&emsp;&emsp;首先如图1需要在项目中添加两份文件：`package.json` 和 `Gruntfile.js`。 
     
1.package.json 文件   
- `package.json` 文件作用   
&emsp;&emsp;`package.json` 文件被 `npm` 用于存储项目的元数据，以便将网站发布为 `npm` 模块。这个文件用来存储 `npm` 模块的依赖项。文件中列出了项目依赖的 `grunt` 和 `Grunt` 插件，放置于 `devDependencies` 配置段内。下面为网站中 `Grunt` 和 `grunt插件` 配置信息：
    ```json
    "devDependencies": {
      "debug": "~0.7.4",
      "grunt": "~0.4.2",
      "grunt-cli": "~0.1.13",
      "grunt-concurrent": "~0.5.0",
      "grunt-contrib-htmlmin": "~0.2.0",
      "grunt-contrib-imagemin": "^0.8.1",
      "grunt-contrib-jshint": "~0.9.2",
      "grunt-contrib-watch": "~0.5.3",
      "grunt-env": "~0.4.1",
      "grunt-jsbeautifier": "^0.2.7",
      "grunt-lesslint": "~1.1.7",
      "grunt-mocha-cov": "~0.2.1",
      "grunt-nodemon": "~0.2.0",
      "jshint-stylish": "~0.1.5",
      "open": "~0.0.5",
      "should": "~3.1.3"
    }
    ```
- `package.json` 文件的位置及创建方式   
&emsp;&emsp; `package.json` 应当放置于项目的根目录中，与Gruntfile在同一目录中，并且应该与项目的源代码一起被提交。在图1 `package.json` 所在目录中运行 `npm install` 将依据 `package.json` 文件中所列出的每个依赖来自动安装适当版本的依赖。

    - 项目创建 `package.json` 文件的方式一般有如下三种：
        1. grunt-init 模版都会自动创建特定于项目的 `package.json`文件；
        2. npm init命令会创建一个基本的 `package.json` 文件；
        3. 复制下面的案例，并根据需要做扩充：
            ```json
            {
                "name": "my-project-name",
                "version": "0.1.0",
                "devDependencies": {
                "grunt": "~0.4.1",
                "grunt-contrib-jshint": "~0.6.0",
                "grunt-contrib-nodeunit": "~0.2.0",
                "grunt-contrib-uglify": "~0.2.2"
            }
            ```

- `package.json` 文件中各字段含义   

    - 以下为网站 `package.json` 文件的配置内容：
        ```json
        {
            "name": "eRealm",
            "description": "Home page for eReaml.",
            "version": "1.0.0",
            "keywords": [
            "open source",
            "node.js",
            "home page"
            ],
            "homepage": "http://www.erealm.cn",
            "author": "dangjian",
            "repository": {
                "type": "git",
                "url": "https://github.com/eRealm/HomeSite.git"
            },
            "config": {
                "unsafe-perm": true
            },
            "bugs": {
                "url": "https://github.com/eRealm/HomeSite/issues",
                "email": "ken@ereaml.com.my"
            },
            "license": "",
            "dependencies": {"express": "^3.4.8"···},
            "devDependencies": {"debug": "~0.7.4"···}
        }
        ```

        - `name` 和 `version`字段是必须的，它们一起组成的标识是唯一的。如果没有就无法安装。    
        - `Description`：网站简介，字符串；     
        - `Keywords`：关键字，数组、字符串；    
        - `Homepage`：网站的url；    
        - `Bugs`：网站项目提交问题的url和邮件地址，对解决问题很有帮助；    
        - `License`：指定一个许可证，让人知道使用和限制的权利；    
        - `Author`：网站开发者；    
        - `Repository`：本网站代码存放的地方，这个对希望贡献的人有帮助；    
        - `Config`：可以用来配置用于包脚本中的跨版本参数；    
        - `Dependencies`：依赖是给一组包名指定版本范围的一个hash，这个版本范围是一个由一个或多个空格分隔的字符串；    
        - `devDependencies`：别人在程序中下载并使用我们的模块时，不用去下载并构建网站使用的外部测试或者文档框架；    

2. 安装grunt插件

    &emsp;&emsp;通过以下命令向已经存在的`package.json`文件中添加`Grunt和grunt`插件。此命令不光安装了`module`，还会自动将其添加到`devDependencies`配置段中。  
    &emsp;&emsp;`npm install <module> --save-dev`   

    &emsp;&emsp;所以网站中，再运用下面这条命令将安装`Grunt`最新版本到项目目录中，并将其添加到`devDependencies`内：    
    &emsp;&emsp;`npm install grunt --save-dev`
    
    &emsp;&emsp;同样，`grunt`插件和其它`node`模块都可以按相同的方式安装。然后在根目录下执行`npm install`将相关的文件下载下来：   

 ![图2](http://i.imgur.com/9SwSc7U.png%22%E5%9B%BE2%22)   
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp; `图 2`
              
3. Gruntfile.js 文件   
    - `Gruntfile.js`文件位置及作用    
    &emsp;&emsp; `Gruntfile.js` 文件是有效的 `JavaScript` 文件，放在项网站根目录中，和 `package.json` 文件在同一目录层级，并和项目源码一起加入源码管理器。 `Gruntfile.js` 文件用于读取 `package` 信息、插件加载、注册任务和运行任务。   

    - `Gruntfile.js`由以下几部分构成：  
    
        1. `"wrapper"` 函数   
            - 网站 `Gruntfile` 文件的 `wrapper` 部分的函数如下:
                ```javascript
                module.exports = function(grunt){
                var pkg = grunt.file.readJSON('package.json');

                grunt.initConfig({
                    pkg: pkg,
                    asset: 'public/asset-'+ pkg.version,
                    bower: {
                        install: {
                        targetDir: "public/vendor",
                        install: true,
                        verbose: true,
                        cleanTargetDir: true,
                        cleanBowerDir: false,
                        bowerOptions: {}
                        }
                    }
                })
                ```
        - 每一份`Gruntfile` 和 `grunt插件`都遵循同样的格式，所有的Grunt代码必须放在此函数内。   
        - 项目的元数据是从 `package.json` 文件中导入到 `Grunt配置` 中的， `grunt.file.readJSON` 方法用于引入 `JSON` 数据。 `grunt-contrib-uglify` 插件中的 `uglify` 任务被配置用于压缩一个源文件以及使用该元数据动态的生成一个 `banner` 注释。见以下代码。   

        2. 项目与任务配置   
            - 如以上 `wrapper` 函数， `Grunt` 任务都依赖某些配置数据，这些数据被定义在一个 `object` 内，并传递给 `grunt.initConfig` 方法。 `grunt.file.readJSON('package.json')` 将存储在 `package.json` 文件中的 `JSON` 元数据引入到 `grunt config` 中。由于 `Gruntfile.js` 是 `javascript` 文件，所以配置信息不只是 `JSON` 格式，这里也可以使用有效的js代码。   
            - 以下为 `package.json` 文件中的 `grunt-contrib-uglify` 插件中的 `uglify` 任务要求它的配置被指定在一个同名属性中。网站使用 `uglify` 任务的 `build` 的目标，用于将多个public目录下的js文件压缩为一个目标文件，即 `libs.min.js` 和 `app.min.js` 文件。
                ```javascript
                uglify: {
                    options:{
                        mangle: true,
                        banner: '/*! <%= pkg.title || pkg.name %> - v<%= pkg.version + "\\n" %>' +
                            '* <%= grunt.template.today("yyyy-mm-dd HH:MM:ss") + "\\n" %>' +
                            '* <%= pkg.homepage + "\\n" %>' +
                            '* Copyright (c) <%= grunt.template.today("yyyy") %> - <%= pkg.author %> */ <%= "\\n" %>'
                    },
                    build: {
                        files: {
                            'public/javascripts/libs.min.js': [
                                'public/javascripts/libs/*.js',
                                'public/javascripts/libs/plugins/jquery.wookmark.min.js',
                                'public/javascripts/libs/plugins/imagesloaded.pkgd.min.js',
                                'public/javascripts/libs/plugins/angular-cookies.min.js',
                                'public/javascripts/libs/plugins/angular-translate.min.js',
                                'public/javascripts/libs/plugins/angular-translate-loader-url.min.js',
                                'public/javascripts/libs/plugins/angular-translate-storage-cookie.min.js',
                                'public/javascripts/libs/plugins/ui-bootstrap-tpls.min.js',
                                'public/javascripts/libs/plugins/ng-mobile-menu.min.js',
                                'public/javascripts/libs/plugins/bootstrap.min.js',
                                'public/javascripts/libs/plugins/moment-with-locales.js'

                            ] ,
                            'public/javascripts/app.min.js': [
                                'public/javascripts/erealm.js',
                                'public/javascripts/language.js',
                                'public/javascripts/clients.js',
                                'public/javascripts/app/*.js'
                            ]
                        }
                    }
                }
                ```
                - 上面代码中 `banner` 中 `<% %>` 分隔符指定的模板会在任务从它们的配置中读取相应的数据时将自动扩展扫描。模板会被递归的展开，直到配置中不再存在遗留的模板相关的信息。运行 `grunt`时， `uglify` 将通过 `banner` 中的 `pkg.title`、 `pkg.name`、`pkg.version` 和 `pkg.homepage` 等匹配加载进来的 `package.json` 中所有数据来生成文件注释。   
                - 当运行一个任务时， `Grunt` 会自动查找配置对象中的同名属性。多任务可以通过任意命名的目标来定义多个配置。如以下代码中的 `jshint` 任务有名为 `client` 和 `sever` 两个目标，同时指定任务和目标，例如 `grunt jshint:client` 或者 `grunt jshint:sever` ，将只会处理指定目标的配置，而运行 `grunt jshint` 将遍历所有目标并依次处理。
                
                ```javascript
                jshint: {
                    options: {
                        reporter: require('jshint-stylish')
                    },
                    client: {
                        options: {
                            jshintrc: '.jshintrc-client',
                            ignores: [
                                'public/javascripts/`/*.min.js'
                            ]
                        },
                        src: [
                            'public/javascripts/`/*.js'
                        ]
                    },
                    server: {
                        options: {
                            jshintrc: '.jshintrc-server'
                        },
                        src: [
                            'config/`/*.js',
                            'app/`/*.js'
                        ]
                    }
                }
                ```
                - 在一个任务配置中， `options` 属性可以用来指定覆盖内置属性的默认值。每一个目标中还可以拥有一个专门针对此目标的 `options` 属性。目标级的 `options` 将会覆盖任务级的 `options`。
      
        3. 加载`grunt`插件和任务   
            - 像 `grunt-contrib-uglify 、grunt-contrib-copy` 等这些常用 `grunt插件` 被加载了进来。只要在 `package.json` 文件中被列为依赖的包，并通过 `npm install` 安装之后，都可以在 `Gruntfile` 中以简单命令的形式使用。如：
                ```javascript
                grunt.loadNpmTasks('grunt-contrib-copy');
                grunt.loadNpmTasks('grunt-contrib-imagemin');
                grunt.loadNpmTasks('grunt-jsbeautifier');

                grunt.loadNpmTasks('grunt-lesslint');
                grunt.loadNpmTasks('grunt-contrib-jshint');
                grunt.loadNpmTasks('grunt-autoprefixer');
                grunt.loadNpmTasks('grunt-filerev');
                grunt.loadNpmTasks('grunt-nodemon');
                grunt.loadNpmTasks('grunt-contrib-watch');
                grunt.loadNpmTasks('grunt-concurrent');

                grunt.loadNpmTasks('grunt-contrib-clean');

                grunt.loadNpmTasks('grunt-contrib-cssmin');
                grunt.loadNpmTasks('grunt-contrib-less');
                grunt.loadNpmTasks('grunt-contrib-concat');
                grunt.loadNpmTasks('grunt-contrib-uglify');
                grunt.loadNpmTasks('grunt-usemin'); 
                ```
        4. 网站中常用`grunt`插件功能介绍   

            &emsp;&emsp;以下为网站中加载的`grunt`插件功能简述：   
            - `grunt-contrib-copy`：用于复制文件或目录，复制src中的文件；   
            - `grunt-contrib-imagemin`：优化并压缩网页图片；   
            - `grunt-contrib-jshint`：用于javascript代码检查，并会给出建议，发布js代码前执行jshint任务，可以避免          - 出现一些低级语法问题；   
            - `grunt-contrib-concat`：用于合并任意文件；   
            - `grunt-contrib-clean`：用于删除文件或目录；   
            - `grunt-contrib-uglify`：用于压缩文件；   
            - `grunt-concurrent`：并发执行任务；   
            - `grunt-contrib-cssmin`：用于网站css文件压缩；   
            - `grunt-contrib-watch`：监听files中文件变动，并自动刷新；   
            - `grunt-usemin`：用来替换模板里的链接为更改后的模板文件的样子；   
            - `grunt-contrib-less`：网站用到Bootstrap，此插件功能是将css文件压缩成less文件；   
            - `grunt-filerev`：对静态资源进行文件重命名；   
            - `grunt-autoprefixer`：解析CSS文件并且添加浏览器前缀到CSS规则里；   
            - `grunt-nodemon`：用于实时监听app.js文件，实现运行grunt后自动启动浏览器以3000端口打开网页； 
  
        5. 自定义任务   
            - 代码中通过定义 `default` 任务，可以让 `Grunt` 默认执行一个或多个任务。在网站中，执行 `grunt` 命令时如果不指定一个任务的话，将会执行 `lesslint,jshint,less:debug, concurrent，autoprefixer:debug` 任务。这和执行 `grunt task`或者 `grunt default` 的效果一样。 `default` 任务列表数组中可以指定任意数目的任务（可以带参数）。
                ```javascript
                grunt.option('force', true);
                grunt.registerTask('prepare', ['copy:main', 'imagemin', 'copy:images', 'clean:images',
                'jsbeautifier']);
                grunt.registerTask('default', ['lesslint', 'jshint','less:debug','autoprefixer:debug',
                "concurrent"]);
                grunt.registerTask('build', ['cssmin', 'less:compile','autoprefixer:compile','uglify',
                'filerev','usemin', 'copy:build', 'clean:build']);
                ```
4. 文件格式

    - 由于大多的任务都是执行文件操作， `Grunt` 有一个强大的抽象层用于声明任务应该操作哪些文件。    
    - `src-dest(源文件-目标文件)` 文件映射的方式有：   
        1. 简洁格式   
        2. 文件对象格式   
        3. 文件数组格式等格式   
    - 这些方式均提供了不同程度的描述和控制操作方式。网站采用的是文件数组格式：   
        ```
        copy: {
            main: {
                files: [
                    {
                        expand: true, cwd: 'public/vendor/jQuery/dist',
                        src: ['jquery.min.map','jquery.min.js'], dest: "public/javascripts/libs"
                    },
                    {
                        expand: true, cwd: 'public/vendor/angular',
                        src: ['angular.min.js.map','angular.min.js'], dest: "public/javascripts/libs"
                    },
                    {
                        expand: true, cwd: 'public/vendor/bootstrap/dist/css',
                        src: ['bootstrap.min.css'], dest: "public/stylesheets/libs"
                    },
                    {
                        expand: true, cwd: 'public/vendor/angular-bootstrap',
                        src: ['ui-bootstrap-tpls.min.js'], dest: "public/javascripts/libs/plugins"
                    },
                    {
                        expand: true, cwd: 'public/vendor/font-awesome/fonts',
                        src: ['`'], dest: "public/stylesheets/fonts"
                    },
                    {
                        expand: true, cwd: 'public/vendor/bootstrap/fonts',
                        src: ['`'], dest: "public/stylesheets/fonts"
                    }
                ]
            }
        ```
    这里让 `copy` 任务将所有存在于src/目录下的文件合并起来，然后存储在dist目录中，并以项目名来命名。

### 相关插件功能配置     
&emsp;&emsp;当所有需要的 `grunt` 插件加载进来后：     
1. `JSHint`  
    - `JSHint` 是Javascript代码验证工具，这种工具可以检查代码并提供相关的代码改进意见。 `JSHint` 只需要一个需要检测的文件数组，然后是一个 `options` 对象，这个对象用于重写 `JSHint` 提供的默认检测规则。如以下代码， `options` 对象中修改了 `JSHint` 默认检测规则，分别使用 `.jshintrc-client` 和 `.jshintrc-sever` 插件，检测public/javascript/目录、config/目录和app/目录下的所有 `.js` 文件并忽略掉该目录下所有 `.min.js` 文件。
        ```javascript
        jshint: {
            options: {
                reporter: require('jshint-stylish')
            },
            client: {
                options: {
                    jshintrc: '.jshintrc-client',
                    ignores: [
                        'public/javascripts/`/*.min.js'
                    ]
                },
                src: [
                    'public/javascripts/`/*.js'
                ]
            },
            server: {
                options: {
                    jshintrc: '.jshintrc-server'
                },
                src: [
                    'config/`/*.js',
                    'app/`/*.js'
                ]
            }
        }
        ```
2. `watch`     
    - 当它检测到任何 `files` 里的文件发生变化时，它就会按照顺序执行 `tasks` 里相应的任务,即刷新。
        ```javascript
        watch: {
            clientHtml: {
                files: ['public/templates/`/*.html'],
                options: {
                    livereload: true
                }
            },
            clientJS: {
                files: [
                    'public/`/*.js', '!client/app/`/*.min.js'
                ],
                tasks: ['newer:jshint:client'],
                options: {
                    livereload: true
                }
            },
            clientLess: {
                files: ['public/stylesheets/`/*.less'],
                tasks:['less:debug','autoprefixer:debug'],
                options: {
                    livereload: true
                }
            }
        }
        ```
3. `copy`      
    - `copy` 任务将public/vendor/jQuery/dist目录下的文件复制到public/javascripts/libs中。
        ```javascript
        copy: {
            main: {
                files: [
                    {
                        expand: true, cwd: 'public/vendor/jQuery/dist',
                        src: ['jquery.min.map','jquery.min.js'], dest: "public/javascripts/libs"
                    },
                    {
                        expand: true, cwd: 'public/vendor/angular',
                        src: ['angular.min.js.map','angular.min.js'], dest: "public/javascripts/libs"
                    }
                ]
            }
        }
        ```
4. `imagemin`     
    - `imagemin` 任务将public/images目录下的所有 `.png、.jpg、.gif` 格式图片优化压缩到public/images-buidl/目录下。
        ```javascript
        imagemin: {
            dynamic: {
                files: [{
                    expand: true,
                    cwd: 'public/images',
                    src: ['`/*.{png,jpg,gif}'],
                    dest: 'public/images-build/'
                }]
            }
        }
        ```
5. `less`        
    - `less` 任务将 `app.css` 文件解析为 `app.less` 文件。
        ```javascript
        less: {
            debug: {
                options: {
                    cleancss: false
                },
                files: {
                    'public/stylesheets/app.css': 'public/stylesheets/app.less'
                }
            },
            compile: {
                options: {
                    cleancss: true
                },
                files: {
                    'public/stylesheets/app.min.css': 'public/stylesheets/app.less'
                }
            }
        }
        ```
&emsp;&emsp;总之 `Grunt` 就是为了自动化。对于前端为了明确模块，我们可以会将 `JavaScript、CSS` 等代码拆解成很多个模块，他们都有独立的一个个文件，但是会导致整个项目文件太多，不利于页面优化。通过 `Grunt` 工具我们将这些文件压缩合并起来，这样我们就能免去很多手动操作，既保证效率又保证质量，高效完成任务。以上只是通过本网站个人初涉 `Grunt` 的一个心得，如有错误欢迎指出。

     

    

