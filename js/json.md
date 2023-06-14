## JSON 的基本概念

### 属性名规范

- 属性名应该一看就知道啥用
- 属性名必须是驼峰，ASCII 码字符串
- 首字符必须是字母，_ （下划线），$(美元符号)
- 避免使用 js 中的保留字
- 数组类型应该是复数，其他属性名都为单数
### 属性值规范

- 属性值应该为四种基本类型（string (字符串)、number (数字）、booleans (布尔值)、null（空））和两个结构化类型（Object (对象)、Arrarys（数组））
### 两个方法

- JSON.parse()
   - 解析一个 JSON 将他转换成 JavaScript 值或对象
- JSON.stringify()
   - 把一个对象或者值转换成 JSON 字符串

### 示例

- JSON 要求在字符串和属性名称周围使用双引号。单引号无效。
```javascript
{
  "squadName" : "Super hero squad",
  "homeTown" : "Metro City",
  "formed" : 2016,
  "secretBase" : "Super tower",
  "active" : true,
  "members" : [
    {
      "name" : "Molecule Man",
      "age" : 29,
      "secretIdentity" : "Dan Jukes",
      "powers" : [
        "Radiation resistance",
        "Turning tiny",
        "Radiation blast"
      ]
    },
    {
      "name" : "Madame Uppercut",
      "age" : 39,
      "secretIdentity" : "Jane Wilson",
      "powers" : [
        "Million tonne punch",
        "Damage resistance",
        "Superhuman reflexes"
      ]
    },
    {
      "name" : "Eternal Flame",
      "age" : 1000000,
      "secretIdentity" : "Unknown",
      "powers" : [
        "Immortality",
        "Heat Immunity",
        "Inferno",
        "Teleportation",
        "Interdimensional travel"
      ]
    }
  ]
}
```
```javascript
<!--./user.JSON-->

{
    "id": 1,
    "name": "John Doe",
    "age": 12
}
```

```javascript
var text = '{ "sites" : [' +
    '{ "name":"Runoob" , "url":"www.runoob.com" },' +
    '{ "name":"Google" , "url":"www.google.com" },' +
    '{ "name":"Taobao" , "url":"www.taobao.com" } ]}';
    
obj = JSON.parse(text);
document.getElementById("demo").innerHTML = obj.sites[1].name + " " + obj.sites[1].url;
```
```javascript
var obj = {a: 'Hello', b: 'World'}; //这是一个js对象，注意js对象的键名也是可以使用引号包裹的,这里的键名就不用引号包含
var json = '{"a": "Hello", "b": "World"}'; //这是一个 JSON 字符串，本质是一个字符串

// JSON（格式字符串） 和 JS 对象（也可以叫 JSON 对象 或 JSON 格式的对象）互转（JSON.parse 和 JSON.stringify）。
// 要实现从 JSON 字符串转换为 JS 对象，使用 JSON.parse () 方法：
var obj = JSON.parse('{"a": "Hello", "b": "World"}'); //结果是 {a: 'Hello', b: 'World'}  一个对象

//要实现从 JS 对象转换为 JSON 字符串，使用 JSON.stringify () 方法：

var json = JSON.stringify({a: 'Hello', b: 'World'}); //结果是 '{"a": "Hello", "b": "World"}'  一个JSON格式的字符串
```

说句不严谨的话：JSON.parse () 就是**字符串**转 **js 对象**， JSON.stringify () 就是 **js 对象**转**字符串**，它们前提是要 json 格式才有意义。
`JSON.stringify(value[, replacer[, space]])`
```javascript
var str = {"name":" 菜鸟教程 ", "site":"http://www.runoob.com"}
str_pretty1 = JSON.stringify(str)
document.write( " 只有一个参数情况：" );
document.write( "<br>" );
document.write("<pre>" + str_pretty1 + "</pre>" );
 
document.write( "<br>" );
str_pretty2 = JSON.stringify(str, null, 4) // 使用四个空格缩进
 document.write( " 使用参数情况：" );
document.write( "<br>" );
document.write("<pre>" + str_pretty2 + "</pre>" ); // pre 用于格式化输出
```
`JSON.parse(text[, reviver])`
```javascript
<p id="demo"></p>

<script>
document.getElementById("demo").innerHTML =
obj.employees[1].name + " " + obj.employees[1].site;
</script>
```
```javascript
JSON.parse('{"p": 5}', function(k, v) {
  if (k === '') { return v; } 
  return v * 2;               
});                          
 
JSON.parse('{"1": 1, "2": 2, "3": {"4": 4, "5": {"6": 6}}}', function(k, v) {
  console.log(k); // 输出当前属性，最后一个为 ""
  return v;       // 返回修改的值
});

```

```javascript
<script>	
    var  params = [];
    for(var i = 0; i < 3; i++){
        var param = [];
        param.push("one");
        param.push("two");
        param.push("three");
        params.push({"group":i,"param":param});
    }

    var json = JSON.stringify(params);
    alert(json);
</script>

// 输出结果是：[{"group":0,"param":["one","two","three"]},{"group":1,"param":["one","two","three"]},{"group":2,"param":["one","two","three"]}]
```
```javascript
var object = {};
var params = [];
    
for(var i = 0; i < 3; i++){
	var obj = {};	
	obj[i] = "abc";
	params.push(obj);
	
}
object['name'] = 'jack';
object['age'] = 25;
object['data'] = params;
 
var json = JSON.stringify(object);

console.log(json);

//输出为：{"name":"jack","age":25,"data":[{"0":"abc"},{"1":"abc"},{"2":"abc"}]}
```
```javascript
var text = '{ "sites" : [' +
  '{ "name":"Learn-anything" , "url":"www.learn-anything.cn" },' +
  '{ "name":"Google" , "url":"www.google.com" },' +
  '{ "name":"Taobao" , "url":"www.taobao.com" } ]}';

obj = JSON.parse(text);
console.log("obj", obj);
```
## JSON 的实际运用
### 引入方式
#### Fetch API
```javascript
<!--./index.js-->

fetch('https://server.com/data.json')
    .then((response) => response.json())
    .then((json) => console.log(json));
```
#### import 方法
```javascript
import cherryJSON  from './data.json' assert { type: 'JSON' };
console.log(data);
let ary = cherryJSON.arrayList
```
Fetch API 通过发送 HTTP 请求来读取 JavaScript 中的 JSON 文件，而 import 语句不需要任何 HTTP 请求，而是像我们所做的其他所有导入一样工作。

#### JS 读取 json 文件
```javascript
<script>
        window.onload = function () {
            var url = "demo.json"/*json文件url，本地的就写本地的位置，如果是服务器的就写服务器的路径*/
            var request = new XMLHttpRequest();
            request.open("get", url);/*设置请求方法与路径*/
            request.send(null);/*不发送数据到服务器*/
            request.onload = function () {/*XHR对象获取到返回信息后执行*/
                if (request.status == 200) {/*返回状态为200，即为数据获取成功*/
                    var json = JSON.parse(request.responseText);
                    for(var i=0;i<json.length;i++){
                        console.log(json[i].name);
                    }
                    console.log(json);
                }
            }
       }
    </script>
```

#### 通过 ajax 获取 json
```javascript
var Ajax = function ()
  {
    $.getJSON ("demo.json", function (data)
               {
                 $.each (data, function (i, item)
                         {
                           console.log(item.name);
                         });
               });
  }();

$.ajax({
  url: "demo.json",//json文件位置，文件名
  type: "GET",//请求方式为get
  dataType: "json", //返回数据格式为json
  success: function(data) {//请求成功完成后要执行的方法 
    //给info赋值给定义好的变量
    var pageData=data;
    for(var i=0;i<data.length;i++){
      console.log(pageData[i].name);
    }
  }
})


```

### 在 Vue 中引用
#### require 引用
```javascript
test.json文件
{
  "testData": "hello world",
  "testArray": [1,2,3,4,5,6],
  "testObj": {
    "name": "tom",
    "age": 18
  }
}
```
```javascript
// require引用：
mounted() {
    // require引用时，放src和放statci都可以，建议放static
    const testJson = require('../../static/json/test.json');
    // const testJson = require('./json/test.json');
    const {testData, testArray, testObj} = testJson;
    console.log('testData',testData);
    // ‘hello world’
    console.log('testArray',testArray);
    // [1,2,3,4,5,6]
    console.log('testObj',testObj);
    //    {
    //    "name": "tom",
    //    "age": 18
    //  }
}
```
```javascript
// import 引用
// import引用时，放src和放statci都可以，建议放static
import testImportJson from '../../static/json/test.json'
// import testImportJson from './json/test.json'
export default {
  data(){
    return{
      testImportJson  
    }
  },
  mounted() {
    const {testData, testArray, testObj} = this.testImportJson;
    console.log('testImportData',testData);
    // ‘hello world’
    console.log('testImportArray',testArray);
    // [1,2,3,4,5,6]
    console.log('testImportObj',testObj);
    //    {
    //    "name": "tom",
    //    "age": 18
    //  }
  }
}
```
```javascript
// http引用
methods:{
  async jsonHttpTest(){
    const res = await this.$http.get('http://localhost:8080/static/json/test.json');
    // 放在src中的文件都会被webpack根据依赖编译，无法作为路径使用，static中的文件才可以作为路径用
    // const res = await this.$http.get('http://localhost:8080/src/page/json/test.json');
    const {testData, testArray, testObj} = res.data;
    console.log('testHttpData',testData);
    // ‘hello world’
    console.log('testHttpArray',testArray);
    // [1,2,3,4,5,6]
    console.log('testHttpObj',testObj);
    //    {
    //    "name": "tom",
    //    "age": 18
    //  }        
  }
},
mounted() {
  this.jsonHttpTest();
},
```
