# css BEM命名规范
[CSS命名规范和模块化的思考 - 掘金](https://juejin.cn/post/6844903736146395143)

## 命名空间：
我认为这可以应用在我们的项目中，提高了代码的可读性。

- 

- **p - 页面（Page）** （应用于 body 元素的类）, 对可维护性不是那么重要的静态页面十分有用 — 应该避免嵌套使用 (例: p-Homepage);
- **l - 布局（Layout）**, 比如列（columning），包裹（wrappers） 和容器（containers）等等 (例: l-Masthead, l-Footer);
- **c - 组件（components ）**(例: c-Dropdown, c-Button…);
- **u - 公共类（Utility classes）** — 不会发生改变，在代码的任何地方都不能重载。(例: u-textCenter, u-clearfix…);
- **js-JavaScript 钩子，**永远不应该出现在 CSS 中。

这些命名空间暂不使用。

- is-，has-：表示一种状态或条件样式。如 .is-active
- o-：表示一个对象（Object），如 .o-layout。
- t-：表示一个主题（Theme），如 .t-light。
- s-：表示一个上下文或作用域（Scope），如 .s-cms-content。
- _：表示一个 hack，如 ._important。
- qa-：表示测试钩子。
## 原则：

- CSS 命名要求：语义化易于理解，可重用性高，后期维护容易，加载渲染快。
- 以英文单词命名，避免无意义的缩写，以 - 连接。根据 BEM 规范，命名格式为 block-element--modifier。
- 在你的结构中要尽量减少类名。
- 不要让你的 CSS 嵌套层级多余三个。
- 包裹容器如何命名：container/list - wrap - item - header - content
-  如果样式的命名让你自己瞄一眼都看不懂又无法改变，请务必注释。
- 所有的 <template> 中的包裹的最高级唯一元素为 < article>，因为在 < article > 中标签可以自动补齐，<div > 不可以。
- 使用有意义的或通用的 ID 和 class 命名。ID 和 class 的命名应反映该元素的功能或使用通用名称，而不要用抽象的晦涩的命名。反映元素的使用目的是首选；使用通用名称代表该元素不表特定意义，与其同级元素无异，通常是用于辅助命名；使用功能性或通用的名称可以更适用于文档或模版变化的情况。



作者：彭薄
链接：https://juejin.cn/post/6844903736146395143
来源：稀土掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。


---

作者：西南_张家辉
链接：[https://juejin.cn/post/6844903672162304013](https://juejin.cn/post/6844903672162304013)
来源：稀土掘金

## 1 什么是 BEM 命名规范

-  **B** - `Block` 一个独立的模块，一个本身就有意义的独立实体 比如：`header`、`menu`、`container`
**E** - `Element` 元素,块的一部分但是自身没有独立的含义 比如：`header title`、`container input`
**M** - `Modifier` 修饰符，块或者元素的一些状态或者属性标志 比如：`small`、`checked` 

### BEM使用

- 知道了`BEM`的基本概念后接下来就是使用了，上面我也说了，说白了`BEM`也就是把三个连接在一起组成一个`class`名,那怎么连接他们三呢？
- `BEM`提出的一个概念是用连接符号来表达,它并不规定必须用什么连接符,但规定用不同连接符做团队内约定区分BEM 3类元素。
- `B`其实可以理解成一个模块，就比如`Element`的`el-button`、`Ant Design`的`ant-btn`。
- `E`的连接用官方的方式就是块名称加两个下划线加元素名称构成（ `__` ）就比如`Element`的`el-radio__input`。
- `M`的连接用官方的方式就是`.block__elem--mod`，就比如`Element`的`el-button--small`、`vant`的`van-button--danger`。

### 总之
> -  中划线 ：仅作为连字符使用，表示某个块或者某个子元素的多单词之间的连接记号。

> __  双下划线：双下划线用来连接块和块的子元素

> _   单下划线：单下划线用来描述一个块或者块的子元素的一种状态

```css
.block {}

.block__element {}

.block--modifier {}
```

每一个块(block)名应该有一个命名空间（前缀）

- `block` 代表了更高级别的抽象或组件。
- `block__element` 代表 .block 的后代，用于形成一个完整的 .block 的整体。
- `block--modifier` 代表 .block 的不同状态或不同版本。

示例：
```html
<div class="article">
    <div class="article__body">
        <div class="tag"></div>
        <button class="article__button--primary"></button>
        <button class="article__button--success"></button>
    </div>
</div>
```

### 推荐写法和风格
```html
.form { }
.form--theme-xmas { }
.form--simple { }
.form__input { }
.form__submit { }
.form__submit--disabled { }

//对应的HTML结构如下：
<form class="form form--theme-xmas form--simple">
  <input class="form__input" type="text" />
  <input
    class="form__submit form__submit--disabled"
    type="submit" />
</form>
```

## 二、常用CSS辅助手册

### **1、常见class关键词**
布局类：header, footer, container, main, content, aside, page, section
包裹类：wrap, inner
区块类：region, block, box
结构类：hd, bd, ft, top, bottom, left, right, middle, col, row, grid, span
列表类：list, item, field
主次类：primary, secondary, sub, minor
大小类：s, m, l, xl, large, small
状态类：active, current, checked, hover, fail, success, warn, error, on, off
导航类：nav, prev, next, breadcrumb, forward, back, indicator, paging, first, last
交互类：tips, alert, modal, pop, panel, tabs, accordion, slide, scroll, overlay
星级类：rate, star
分割类：group, seperate, divider
等分类：full, half, third, quarter
表格类：table, tr, td, cell, row
图片类：img, thumbnail, original, album, gallery
语言类：cn, en
论坛类：forum, bbs, topic, post
方向类：up, down, left, right
其他语义类：btn, close, ok, cancel, switch; link, title, info, intro, more, icon; form, label, search, contact, phone, date, email, user; view, loading...

### 2、常用的CSS命名规则
头：header　　内容：content/container　　尾：footer　　导航：nav　　侧栏：sidebar
栏目：column　　页面外围控制整体布局宽度：wrapper　　左右中：left right center
登录条：loginbar　　标志：logo　　广告：banner　　页面主体：main　　热点：hot
新闻：news　　下载：download　　子导航：subnav　　菜单：menu
子菜单：submenu　　搜索：search　　友情链接：friendlink　　页脚：footer
版权：copyright　　滚动：scroll　　内容：content　　标签页：tab
文章列表：list　　提示信息：msg　　小技巧：tips　　栏目标题：title
加入：joinus　　指南：guild　　服务：service　　注册：regsiter
状态：status　　投票：vote　　合作伙伴：partner

#### (1)页面结构
容器: container　　页头：header　　内容：content/container
页面主体：main　　页尾：footer　　导航：nav
侧栏：sidebar　　栏目：column　　页面外围控制整体布局宽度：wrapper
左右中：left right center


#### (2)导航
导航：nav　　主导航：mainbav　　子导航：subnav
顶导航：topnav　　边导航：sidebar　　左导航：leftsidebar
右导航：rightsidebar　　菜单：menu　　子菜单：submenu
标题: title　　摘要: summary

#### (3)功能
标志：logo　　广告：banner　　登陆：login　　登录条：loginbar
注册：regsiter　　搜索：search　　功能区：shop
标题：title　　加入：joinus 　状态：status　　按钮：btn
滚动：scroll　　标签页：tab　　文章列表：list　　提示信息：msg
当前的: current　　小技巧：tips　　图标: icon　　注释：note
指南：guild　服务：service　　热点：hot　　新闻：news
下载：download　　投票：vote　　合作伙伴：partner
友情链接：link　　版权：copyright

### 3、**CSS样式表文件命名**
主要的 master.css
模块 module.css
基本共用 base.css
布局、版面 layout.css
主题 themes.css
专栏 columns.css
文字 font.css
表单 forms.css
补丁 mend.css
打印 print.css

### 4、修改类名-取名规范

**(1)颜色:使用颜色的名称或者16进制代码,如**
.red { color: red; }
.f60 { color: #f60; }
.ff8600 { color: #ff8600; }

**(2)字体大小,直接使用’font+字体大小’作为名称,如**
.font12px { font-size: 12px; }
.font9pt {font-size: 9pt; }

**(3)对齐样式,使用对齐目标的英文名称,如**
.left { float:left; }
.bottom { float:bottom; }

**(4)标题栏样式,使用’类别+功能’的方式命名,如**
.barnews { }
.barproduct { }
