# Yarn使用指南



#### 创建一个新项目

```
yarn init
复制代码
```

接着提示一下

```
name (your-project):
version (1.0.0):
description:
entry point (index.js):
git repository:
author:
license (MIT):
复制代码
```

生成 package.json 文件

```
{
  "name": "my-new-project",
  "version": "1.0.0",
  "description": "My New Project description.",
  "main": "index.js",
  "repository": {
    "url": "https://example.com/your-username/my-new-project",
    "type": "git"
  },
  "author": "Your Name <you@example.com>",
  "license": "MIT"
}
复制代码
```

#### 思维导图 方便记忆

![yarn and npm](/_images/code/yarn.webp)





#### 添加、更新、删除依赖

```
yarn / yarn install 一键安装jpackage.json所有包
yarn add [package] — 添加包，会自动安装最新版本，注意会覆盖指定版本号！！！
yarn add [package]@[version] — 带版本号安装
yarn remove [package] 移除某个包
yarn upgrade [package] 更新一个包
yarn add vue 安装一个包
yarn add vue@2.5.0  安装一个包
yarn upgrade vue 更新一个包
yarn upgrade vue@3.0.0 指定更新某个版本的包
yarn remove vue 

yarn add vue 安装到dependencies
yarn add vue --save-dev 安装到devDependencies
复制代码
```



#### npm 和 yarn 比较

| npm                                  | yarn                          | 用法                           |
| ------------------------------------ | ----------------------------- | ------------------------------ |
| npm install                          | yarn install                  | 一键安装 package.json 的所有包 |
| npm install [package] --save / -S    | yarn add [package]            | 安装到 dependencies            |
| npm install [package] --save-dev/ -D | yarn add [package] --save-dev | 安装到 devDependencies         |
| npm i [package]@[版本号]             | yarn add [package]@[版本号]   | 指定版本号下载更新             |
| npm install [package] --global       | yarn global add [package]     | 全局安装某个包                 |
| npm update --global                  | yarn updade upgrade           | 更新所有包                     |
| npm uninstall [package]              | yarn remove [package]         | 删除某个包                     |




### yarn 和 npm 命令对比

| 作用           | npm                                | yarn                 |
| -------------- | ---------------------------------- | -------------------- |
| 安装           | npm install/i                      | yarn                 |
| 卸载           | npm unintall/un                    | yarn remove          |
| 全局安装       | npm i xxx --global/-g              | yarn global add xxx  |
| 安装包         | npm i xxx --save/-S                | yarn add xxx         |
| 开发模式安装包 | npm i xxx --save-dev/-D            | yarn add xxx -dev/-D |
| 更新           | npm update                         | yarn upgrade         |
| 全局更新       | npm update -g                      | yarn global upgrade  |
| 卸载           | npm un xxx                         | yarn remove xxx      |
| 清除缓存       | npm cache clean                    | yarn cache clean     |
| 重装           | rm -rf node_modules && npm install | yarn upgrade         |




来源：稀土掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

作者：Taomi
链接：https://juejin.cn/post/6844903850210492423

作者：SpeeUI
链接：https://juejin.cn/post/6844903764453769229


