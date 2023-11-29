## 什么是 Strapi？
[https://www.strapi.cn/dev-docs/quick-start](https://www.strapi.cn/dev-docs/quick-start)

无头CMS（Headless CMS）

Strapi完全由[JavaScript](https://www.chengzz.com/tag/javascript)开发，基于[Node.js](https://www.chengzz.com/tag/node-js)构建，通过配置数据库和内容类型，即可快速搭建出色的内容管理系统。开发者可以选择使用内置的内容类型，也可以自定义内容类型来管理任何类型的数据。Strapi不仅仅取悦工程师，还注重人性化设计。它提供了友好的用户界面和易于使用的[API](https://www.chengzz.com/tag/api)，既减轻了开发工作，又提升了用户体验。
## 教程参考：

官网：
[https://docs.strapi.io/dev-docs/quick-start](https://docs.strapi.io/dev-docs/quick-start)

推荐先看
[使用 strapi 快速构建 API 和 CMS 管理系统 - 掘金](https://juejin.cn/post/7205930226445991973)

[GitHub - AutumnFish/strapi_study: 记录自己学习Strapi的过程](https://github.com/AutumnFish/strapi_study)

[欢迎使用 Strapi 开发者文档！ | Strapi 中文网](https://strapi.nodejs.cn/dev-docs/intro)


[图文并茂strapi4.5.5自定义搭建指南以及数据库字段名接口返回mapping分析 - 掘金 - 使用mysql](https://juejin.cn/post/7186297156788535333)


[配置及使用 Strapi CMS 的一些总结](https://www.pipipi.net/29235.html)

[strapi v4版本 快速使用 中文设置 - yjxQWQ - 博客园](https://www.cnblogs.com/xxdmua/articles/17358103.html)

[新手入坑：strapi官网教程的简单示例学习_font-size的博客-CSDN博客](https://blog.csdn.net/qq_36812165/article/details/115533628)

## 安装
在开始使用之前我们需要确保自己的 Node.js 版本为 v14、v16或者 v18，npm 的版本为 v6，如果需要使用到 SQLite 作为数据库的话，还需要在自己的电脑上安装 Python。
### npx
```vue
npx create-strapi-app@latest my-project --quickstart
```
### Yarn
```bash
yarn create strapi-app my-project --quickstart

//yarn create strapi-app my-project
//选择安装类型：
//Quickstart (recommended)，它使用默认数据库 （SQLite）
//Custom (manual settings)，这允许选择您的首选数据库
//启动

yarn develop

//因为strapi版本的问题如果遇到error strapi.start is not a function的错误可以使用yarn develop来启动strapi.

```
因为strapi版本的问题如果遇到error strapi.start is not a function的错误可以使用yarn develop来启动strapi.
```bash
� Start creating your Strapi application.

? Choose your installation type Custom (manual settings)
? Choose your main database: MongoDB
? Database name: blog
? Host: 127.0.0.1
? +srv connection: false
? Port (It will be ignored if you enable +srv): 27017
? Username: blog
? Password: ********
? Authentication database (Maybe "admin" or blank): blog
? Enable SSL connection: false

⏳ Testing database connection...
It might take a minute, please have a coffee ☕️
(node:3108) DeprecationWarning: current Server Discovery and Monitoring engine is deprecated, and will be removed in a future version. To use the new Server Discover and Monitoring engine, pass option { useUnifiedTopology: true } to the MongoClient constructor.

The app has been connected to the database successfully!

�  Application generation:
√ Copy dashboard
√ Install plugin settings-manager.
√ Install plugin content-type-builder.
√ Install plugin content-manager.
√ Install plugin users-permissions.
√ Install plugin email.
√ Install plugin upload.
√ Link strapi dependency to the project.

� Your new application gatsby-blog is ready at D:\WorkSpace\gatsby\strapi-gatsby-starter\gatsby-blog.

⚡️ Change directory:
$ cd gatsby-blog

⚡️ Start application:
$ strapi start
```
## 常见问题
### 汉化问题
[strapi V4安装设置中文面板](https://www.cnblogs.com/zhaoyun4122/p/16246376.html)

### strapi 的post请求
[strapi如何使用](https://www.cnblogs.com/xxdmua/articles/17358103.html)
```bash
function createcommit(name,time,up,down,contant){

  const data = {
    name: name,
    time: time,
    up: up,
    down: down,
    contant: contant
  };
  const data2= {
    data:data
  }
  $.ajax({
    type: 'POST',
    url: 'http://localhost:1337/api/comment-area-managements',
    data: data2,
    success: function(response) {
      console.log(response);
    },
    error: function(error){
      console.log(error);
    }
  });
}
```
