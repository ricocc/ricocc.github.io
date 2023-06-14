<a name="uPmBa"></a>
## localStorage 介绍
是一个用来做本地持久化存储的 Web Api。 localStorage 以为标准的键值对（Key-Value, 简称 KV）数据类型的形式存储数据，在谷歌 Chrome 中，每个域的存储空间最大为 5 MB。<br />解决了 cookie 存储空间不足的问题 (cookie 中每条 cookie 的存储空间为 4k)<br />另外还有 sessionStorage，主要区别是浏览器存储数据的时间，使用 sessionStorage，一旦会话结束或浏览器关闭，数据就会被删除。但是，localStorage 中的数据会一直保存到清除为止。
<a name="IgOXu"></a>
## 常见 API 
我们可以Chrome 浏览器的控制台输入 localStorage 来查看其自带的方法。<br />摘录了一些常用的 API 如下表所示：

| 名称 | 作用 |
| --- | --- |
|  clear |  清空 localStorage 上存储的数据 |
|  getItem |  读取数据 |
|  hasOwnProperty |  检查 localStorage 上是否保存了变量 x，需要传入 x |
| key |  读取第 i 个数据的名字或称为键值 (从 0 开始计数) |
| length | localStorage 存储变量的个数 |
|  propertyIsEnumerable |  用来检测属性是否属于某个对象的 |
|  removeItem |  删除某个具体变量 |
|  setItem |  存储数据 |
|  toLocaleString |  将（数组）转为本地字符串 |
|  valueOf |  获取所有存储的数据 |

<a name="px7oz"></a>
## 常用的用法：
```javascript
// 设置
localStorage.setItem('myCat', 'Tom');

// 获取
let cat = localStorage.getItem('myCat');

// 移除
localStorage.removeItem('myCat');

// 移除所有
localStorage.clear();

if (!window.localStorage) {
  console.log('浏览器版本太低，不支持localStorage')
} else {
  let storage = window.localStorage
  storage.setItem('a', 1) // 存储名为a值为1的变量
  storage.b = 2           // 存储名为b值为2的变量
  storage['c'] = 3        // 存储名为c值为3的变量
}

```

**读取数据**
```javascript
localStorage.getItem("name") //caibin,读取保存在localStorage对象里名为name的变量的值
localStorage.name // "caibin"
localStorage.valueOf() //读取存储在localStorage上的所有数据
localStorage.key(0) // 读取第一条数据的变量名(键值)
//遍历并输出localStorage里存储的名字和值
for(var i=0; i<localStorage.length;i++){
    console.log('localStorage里存储的第'+i+'条数据的名字为：'+localStorage.key(i)+',值为：'+localStorage.getItem(localStorage.key(i)));
}

-------------------------------------

storage.getItem('a') // 1 读取保存在storage对象里名为a的变量值
storage.b            // 2 读取保存在storage对象里名为b的变量值
storage['c']         // 3 读取保存在storage对象里名为c的变量值
storage.key(0)       // 1 根据key值读取数据,key(0)代表对象的第一条数据
storage.valueOf()    // 读取保存在storage对象上的全部数据
```
修改和删除

```javascript
//修改数据
if (!window.localStorage) {
  console.log('浏览器版本太低，不支持localStorage')
} else {
  let storage = window.localStorage
  // 写入a字段
  storage.a = 1
  // 修改a字段
  storage.a = '@Demi'
}

//删除变量
localStorage.removeItem("name"); //undefined
localStorage // Storage {length: 0} 可以看到之前保存的name变量已经从localStorage里删除了

---------------------------------------------------

if (!window.localStorage) {
  console.log('浏览器版本太低，不支持localStorage')
} else {
  let storage = window.localStorage
  storage.clear()         // 删除所有键值对
  storage.removeItem('a') // 删除指定的键值对
}

//检查 localStorage 里是否保存某个变量
localStorage.hasOwnProperty('name') // true
localStorage.hasOwnProperty('sex')  // false

//数组转为本地字符串
var arr = ['aa','bb','cc']; // ["aa","bb","cc"]
localStorage.arr = arr //["aa","bb","cc"]
localStorage.arr.toLocaleString(); // "aa,bb,cc


```

<a name="hfsEF"></a>
### 将 JSON 存储到 localStorage 里
```javascript
var students = {
    xiaomin: {
        name: "xiaoming",
        grade: 1
    },
    teemo: {
        name: "teemo",
        grade: 3
    }
}

students = JSON.stringify(students);  //将JSON转为字符串存到变量里
console.log(students);
localStorage.setItem("students",students);//将变量存到localStorage里

var newStudents = localStorage.getItem("students");
newStudents = JSON.parse(students); //转为JSON
console.log(newStudents); // 打印出原先对象

---------------------------------------------

if (!window.localStorage) {
  console.log('浏览器版本太低，不支持localStorage')
} else {
  let storage = window.localStorage
  let data = {
     name: 'Demi',
     sex: 'woman',
     hobby: 'program'
  }
  // 将对象转换成JSON格式存入localStorage
  let dataValue = JSON.stringify(data)
  storage.setItem('data', dataValue)
 
  // 从localstorage中取出数据转换成对象格式
  let json = storage.getItem('data')
  let jsonObj = JSON.parse(json)
}
```
<a name="zvPhA"></a>
### 监听 LocalStorage 变化
localStorage 被改变时 (从无到有，从有到无，值改变)，会触发一个 storage 事件。我们可以在 window 上监听到这个事件。
```javascript
window.addEventListener('storage', () => {
  ...
});

window.onstorage = () => {
  ...
};
```
这里需要注意的是，在改变 localStorage 的当前页面，是无法监听到 storage 事件的。如果我同时打开了多个**同源**的页面: A 页面、B 页面、C 页面，当在 A 页面中修改 localstorage 时，B 页面和 C 页面中都可以监听到 storage 事件，而 A 页面是不会触发 storage 事件的。



<a name="rsmrg"></a>
## 优缺点
<a name="SZn3E"></a>
#### 优势：
1、localStorage 是以『源 (origin)』为维度进行存储的。也就是说，跨域访问其他站点的 localStorage 是行不通的。<br />2、localStorage 是以字符串的形式保存数据的。<br />3、对于每一个域，localStorage 最多允许存储几 M 数量级的数据 (具体数字因浏览器而异)。<br />localStorage 可以用来做什么：<br />存储登录 token，用户信息等数据；本地持久化保存业务数据；页面同步；保存代码，以提高网站性能。
<a name="nkuAq"></a>
#### 局限：

- 浏览器的大小不统一，并且在 IE8 以上的 IE 版本才支持 localStorage 这个属性
- 目前所有的浏览器中都会把 localStorage 的值类型限定为 string 类型，这个在对我们日常比较常见的 JSON 对象类型需要一些转换
- localStorage 在浏览器的隐私模式下面是不可读取的
- localStorage 本质上是对字符串的读取，如果存储内容多的话会消耗内存空间，会导致页面变卡
- localStorage 不能被爬虫抓取到
- localStorage 与 sessionStorage 的唯一一点区别就是 localStorage 属于永久性存储，而 sessionStorage 属于当会话结束的时候，sessionStorage 中的键值对会被清空



[你可能不知道的LocalStorage用法](https://segmentfault.com/a/1190000020061167)

