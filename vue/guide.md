# Vue -渐进式JavaScript框架

作为自己离线版本方便查询和快速阅览。

看文请支持原作者

作者：小小坤
链接：https://juejin.cn/post/6844903548870721549
来源：掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

## 介绍

- [vue 中文网](https://link.juejin.cn?target=https%3A%2F%2Fcn.vuejs.org%2F)
- [vue github](https://link.juejin.cn?target=https%3A%2F%2Fgithub.com%2Fvuejs%2Fvue)
- Vue.js 是一套构建用户界面(UI)的渐进式JavaScript框架

## 库和框架的区别

- [我们所说的前端框架与库的区别？](https://link.juejin.cn?target=https%3A%2F%2Fzhuanlan.zhihu.com%2Fp%2F26078359%3Fgroup_id%3D830801800406917120)

### Library

> 库，本质上是一些函数的集合。每次调用函数，实现一个特定的功能，接着把`控制权`交给使用者

- 代表：jQuery
- jQuery这个库的核心：DOM操作，即：封装DOM操作，简化DOM操作

### Framework

> 框架，是一套完整的解决方案，使用框架的时候，需要把你的代码放到框架合适的地方，框架会在合适的时机调用你的代码

- 框架规定了自己的编程方式，是一套完整的解决方案
- 使用框架的时候，由框架控制一切，我们只需要按照规则写代码

### 主要区别

- You call Library, Framework calls you
- 核心点：谁起到主导作用（控制反转）
  - 框架中控制整个流程的是框架
  - 使用库，由开发人员决定如何调用库中提供的方法（辅助）
- 好莱坞原则：Don't call us, we'll call you.
- 框架的侵入性很高（从头到尾）

## MVVM的介绍

- MVVM，一种更好的UI模式解决方案
- [从Script到Code Blocks、Code Behind到MVC、MVP、MVVM - 科普](https://link.juejin.cn?target=http%3A%2F%2Fwww.cnblogs.com%2Findream%2Fp%2F3602348.html)

### MVC

- M: Model 数据模型（专门用来操作数据，数据的CRUD）
- V：View 视图（对于前端来说，就是页面）
- C：Controller 控制器（是视图和数据模型沟通的桥梁，用于处理业务逻辑）

### MVVM组成

- MVVM ===> M / V / VM
- M：model数据模型
- V：view视图
- VM：ViewModel 视图模型

### 优势对比

- MVC模式，将应用程序划分为三大部分，实现了职责分离
- 在前端中经常要通过 JS代码 来进行一些逻辑操作，最终还要把这些逻辑操作的结果现在页面中。也就是需要频繁的操作DOM
- MVVM通过`数据双向绑定`让数据自动地双向同步
  - V（修改数据） -> M
  - M（修改数据） -> V
  - 数据是核心
- Vue这种MVVM模式的框架，不推荐开发人员手动操作DOM

### Vue中的MVVM

> 虽然没有完全遵循 MVVM 模型，Vue 的设计无疑受到了它的启发。因此在文档中经常会使用 vm (ViewModel 的简称) 这个变量名表示 Vue 实例

### 学习Vue要转化思想

- 不要在想着怎么操作DOM，而是想着如何操作数据！！！




