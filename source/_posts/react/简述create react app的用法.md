---
title: 简述create react app的用法
date: 2019-09-24 00:00:00
categories:
  - react
cover: >-
  https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1570615514153&di=6f99e51380c6212468e4565b6321a633&imgtype=0&src=http%3A%2F%2Fpic4.zhimg.com%2Fv2-38bdac71902e51febd1ab576a32c0616_1200x500.jpg
---

### 详细用法

1. 全局安装

    `npm i create-react-app -g`
    
2. 创建应用（以下其一即可）

    - `npx create-react-app my-app`
    - `yarn create create-react-app my-app`
    - `npm i create-react-app my-app`

3. 将封装在 `create-react-app` 中的配置全部反编译到当前项目中，使用户完全取得 `webpack` 文件的控制权

    `npm run eject` 或 `yarn eject`

    **你不会想要用到这个命令的**

4. 运行测试

    `npm run test` 或 `yarn test`

5. 编译

    `npm run build` 或 `yarn build`

6. 运行程序

    ```bash
    cd my-app
    npm/yarn start
    ```

### 推荐阅读

- [官方网站](https://create-react-app.dev)

 

