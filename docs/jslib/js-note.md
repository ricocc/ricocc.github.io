# 代码块

## 1. 前端JS无缝滚动

工作中网页会有特定场景需要用到滚动的需求，记录一下最后选择的方式
参考文章： [前端js无缝滚动---解决两个小bug](https://blog.csdn.net/qq_34831149/article/details/86678848)
目前应用到的页面是  [ukrainebeauty.net/12](https://www.ukrainebeauty.net/qa/register12.php)  和  [ukrainebeauty.net/14](https://www.ukrainebeauty.net/qa/register14.php)
元素fixed+absolute定位作为背景，同时不影响背景颜色和效果的呈现
为了方便控制大小和不受页面定位方式影响，图片作为背景铺满

HTML结构
```html
<div class="lady-box">
		<div class="lady-list lady-list-1" >
			<div class="lady-item lady-1" style="background:url('register12/images/01.jpg') no-repeat center center;"></div>
			<div class="lady-item lady-2" style="background:url('register12/images/02.jpg') no-repeat center center;"></div>
			<div class="lady-item lady-3" style="background:url('register12/images/01-girl.gif') no-repeat center center;"></div>
			<div class="lady-item lady-4" style="background:url('register12/images/03.jpg') no-repeat center center;"></div>
			<div class="lady-item lady-5" style="background:url('register12/images/05.jpg') no-repeat center center;"></div>
			<div class="lady-item lady-6" style="background:url('register12/images/03-girl.gif') no-repeat center center;"></div>
			<div class="lady-item lady-7" style="background:url('register12/images/07.jpg') no-repeat center center;"></div>
			<div class="lady-item lady-8" style="background:url('register12/images/02-girl.gif') no-repeat center center;"></div>
		</div>
</div>
```

JS代码
```javascript
$(".lady-list-1").clone().addClass("lady-list-2").removeClass("lady-list-1").appendTo(".lady-box");
		var offHeight = $('.lady-list').height(); //获取向上滚动的距离
        var childrenlength = $(".lady-list").length;//元素数量
        stylecss = "@keyframes move {" +
        "    from {transform: translate(0px,0px)}" +
        "    to {transform: translate(0px,-"+offHeight+"px)}" +
        "}"+
        "@-moz-keyframes move {" +
        "    from {transform: translate(0px,0px)}" +
        "    to {transform: translate(0px,-"+offHeight+"px)}" +
        "}"+
        "@-webkit-keyframes move {" +
        "    from {transform: translate(0px,0px)}" +
        "    to {transform: translate(0px,-"+offHeight+"px)}" +
        "}"+
        "@-o-keyframes move {" +
        "    from {transform: translate(0px,0px)}" +
        "    to {transform: translate(0px,-"+offHeight+"px)}" +
        "}"
    ;
        var style = document.createElement('style');
        style.type = 'text/css';
        style.innerHTML = stylecss;
        document.getElementsByTagName('head')[0].appendChild(style);
        this.stylesheet = document.styleSheets[document.styleSheets.length-1];
        $('.lady-box').css({
            //'animation':'move '+(offHeight/childrenlength)+'s infinite',  //滚动的时间及方式
			'animation':'move 35s infinite',  //自定义动画时间和速度
            "animation-timing-function":"linear"
        });
```

## 2. JQ 模拟在线人数自动变化

```javascript
// 在线人数自动变化插件
(function($){
  $(document).ready(function(){
// 创建构造函数
// ele是元素， opt是文档（JQ所有文档内容）
    var onlineChange=function(ele,opt,basic,num){
        this.ele = $(ele);
        //定义用户可更改的默认值
        this.defaults ={
            basic:['2000','3000','40000'],
            num:'5',
            time:'300'
        };
        this.settings = $.extend({},this.dedaults,opt);

    }
    onlineChange.prototype ={
        //初始化函数，页面加载之前就要添加所有的事件
        change:function(){
            var _this = this;
            basic = _this.settings.basic;
            num = _this.settings.num;
            time = _this.settings.time;
            var length = _this.ele.length;
            let count, random_n;

            function auto_count(){
                for(let i = 0;i<=length;i++){
                    randow_n = Math.floor((Math.random()*num));
                    count= Math.floor(basic[i])+randow_n;
                    _this.ele.eq(i).text(count);
                }

            }
            setInterval(auto_count,time);
        }
    }

    $.fn.onlineNum = function(option){
        var  onlinechange = new  onlineChange(this,option)
        return  onlinechange.change();
    }
 });
})(jQuery);

//调用
$(document).ready(function(){
    $('.online-num').onlineNum({//调用函数
            basic:['4329'],//顺序排列在线人数基数
            num:'100',//随机增长的数值范围,示例[0，100];
            time:'2000' //自动变动时间，1000=1秒
    });
});
```

## 3. JQ 鼠标移动元素位移
```javascript
window.onload = function(){
    document.onmousemove = function(event){
        var left = event.clientX/130 +'px';
        var　top = event.clientY/130+'px';
        var　z = event.clientX/100+'px';
        $(".steps .step:first-child").css("transform","translate3d("+left+","+top+","+z+")");
    };
};
```

## 4. 原生 JS  倒计时
```javascript
/* num count */
var count = 4;
var counter = setInterval(timer, 1000);

function timer() {
  count = count - 1;
  if (count <0) {
    clearInterval(counter);
    return;
  }
  document.getElementById("timer").innerHTML = "("+count + "s)";
}
```

HTML 部分
```html
<span id="timer"> </span>
```

## 5. JQ 监听页面滚动加载元素
```html
class="revealOnScroll ani animated" data-animation="ani" data-timeout="50"
```

```javascript
$(function() {
    //scroll_animation

    var $window = $(window),

        win_height_padded = $window.height() * 0.93;

    $window.on('scroll', revealOnScroll);



    function revealOnScroll() {

        var scrolled = $window.scrollTop();

        $(".revealOnScroll:not(.animated)").each(function() {

            var $this = $(this),

                offsetTop = $this.offset().top;



            if (scrolled + win_height_padded > offsetTop) {

                if ($this.data('timeout')) {

                    window.setTimeout(function() {

                            $this.addClass('animated ' + $this.data('animation'));

                        },

                        parseInt($this.data('timeout'), 10));

                } else {

                    $this.addClass('animated ' + $this.data('animation'));

                }

            }

        });

    }

    function getDataset(ele){
        if(ele.dataset){
            return ele.dataset;
        }else{
            var attrs = ele.attributes,//元素的属性集合
                dataset = {},
                name,
                matchStr;
    
            for(var i = 0;i<attrs.length;i++){
                //是否是data- 开头
                matchStr = attrs[i].name.match(/^data-(.+)/);
                if(matchStr){
                    //data-auto-play 转成驼峰写法 autoPlay
                    name = matchStr[1].replace(/-([\da-z])/gi,function(all,letter){
                        return letter.toUpperCase();
                    });
                    dataset[name] = attrs[i].value;
                }
            }
            return dataset;
        }
    }

});
```

## 6. JS 判断移动端设备
```javascript
$(function(){
  try {
    var urlhash = window.location.hash;
    if (!urlhash.match("fromapp")){
      if ((navigator.userAgent.match(/(iPhone|iPod|Android)/i))){
          // 移动端
      }else{
		  // PC 端
      }
    }
  }
  catch(err){}

});
```

## 7. CSS + JS 修改鼠标指针 cursor - 跟随交互
参考这个站点的做法，实现代码。

直接定位`cursor`
```html
<style>
* {
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
}
  
.cursor {
    position: fixed;
    left: 0;
    top: 0;
    right: 0;
    bottom: 0;
    z-index: 9999999;
    display: -webkit-box;
    display: -webkit-flex;
    display: -ms-flexbox;
    display: flex;
    width: 100%;
    height: 100vh;
    -webkit-box-pack: center;
    -webkit-justify-content: center;
    -ms-flex-pack: center;
    justify-content: center;
    -webkit-box-align: center;
    -webkit-align-items: center;
    -ms-flex-align: center;
    align-items: center
}

.cursor__dot {
    display: -webkit-box;
    display: -webkit-flex;
    display: -ms-flexbox;
    display: flex;
    width: 1em;
    height: 1em;
    max-height: 14px;
    max-width: 14px;
    -webkit-box-pack: center;
    -webkit-justify-content: center;
    -ms-flex-pack: center;
    justify-content: center;
    -webkit-box-align: center;
    -webkit-align-items: center;
    -ms-flex-align: center;
    align-items: center;
    border: 1px #1d1d1d;
    border-radius: 500px;
    background-color: hsla(0, 0%, 100%, .01);
    opacity: 1;
    -webkit-backdrop-filter: invert(100%);
    backdrop-filter: invert(100%);
    -webkit-transition: height 350ms, width 350ms, opacity 350ms, max-height 350ms, max-width 350ms, -webkit-filter 350ms;
    transition: filter 350ms, height 350ms, width 350ms, opacity 350ms, max-height 350ms, max-width 350ms, -webkit-filter 350ms;
    color: #1d1d1d
}

.cursor__dot.is--mail {
    width: 10em;
    height: 10em;
    max-height: 10em;
    max-width: 10em
}

.cursor__dot.is--case {
    width: 12em;
    height: 12em;
    max-height: 12em;
    max-width: 12em;
    background-color: #f8f8f8;
    -webkit-backdrop-filter: invert(0%);
    backdrop-filter: invert(0%)
}

.cursor__dot.is--text__link {
    width: 3em;
    height: 3em;
    max-height: 3em;
    max-width: 3em
}

.cursor__text--mail {
    display: none;
    font-weight: 400
}

.cursor__text--mail.visible {
    display: block
}
  
</style>
<!-- html 部分 -->
<div class="cursor">
  <div class="cursor__dot" >
    <div class="cursor__text--mail">EMAIL</div>
    <div class="cursor__text--case">SEE CASE</div>
  </div>
</div>


<script>
// custom classes for cursor
  $('.footer__link__wrapper').on('mouseenter mouseleave', function() {
     $('.cursor__dot').toggleClass('is--mail');
     $('.cursor__text--mail').toggleClass('visible');
  });

  $('.project__link').on('mouseenter mouseleave', function() {
     $('.cursor__dot').toggleClass('is--case');
     $('.cursor__text--case').toggleClass('visible');
  });

  $('.text__link , .footer__link , .nav__logo , .button , .nav__btn').on('mouseenter mouseleave', function() {
     $('.cursor__dot').toggleClass('is--text__link');
});
</script>
```




_参考阅读：_
[有意思的鼠标指针交互探究](https://juejin.cn/post/7111517270899163172)
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>鼠标跟随交互实战</title>
    <style>
      .wrapper{
        width: 100%;
        margin:0 auto;
      }
      .container{
        max-width: 80%;
        margin: 0 auto;
      }
      .white{
        background-color: #fff;
        width: 100%;
        height: 300px;
      }
      .black{
        background-color: #202020;
        width: 100%;
        height: 300px;
      }
    </style>
    <style>
      body{
        cursor: none;
      }
      
      #g-pointer-1,
      #g-pointer-2
      {
        position: absolute;
        top: 0;
        left: 0;
        width: 12px;
        height: 12px;
        background: #999;
        border-radius: 50%;
        background-color: #fff;
        mix-blend-mode: exclusion;
        z-index: 9999;
        pointer-events: none;
      }
      #g-pointer-2 {
        display: none;
        width: 42px;
        height: 42px;
        background: #222;
        transition: .2s ease-out;
      }
      .white:hover #g-pointer-2{
        display: block;
        
      }
    </style>
  </head>
  <body>
    <div id="wrapper">
      <div class="container white"><div id="g-pointer-2"></div></div>
      <div class="container black "></div>
    </div>
    <!-- =====================================
        鼠标正式内容
        ====================================== -->
    <div id="g-pointer-1"></div>
    
    <script>
      const body = document.querySelector("body");
      const element = document.getElementById("g-pointer-1");
      const element2 = document.getElementById("g-pointer-2");
      const halfAlementWidth = element.offsetWidth / 2;
      const halfAlementWidth2 = element2.offsetWidth / 2;
      
      function setPosition(x, y) { 
        element.style.transform  = `translate(${x - halfAlementWidth}px, ${y - halfAlementWidth}px)`;       element2.style.transform  = `translate(${x - halfAlementWidth2}px, ${y - halfAlementWidth2}px)`;
      }
      
      body.addEventListener('mousemove', (e) => {
        window.requestAnimationFrame(function(){
          setPosition(e.clientX, e.clientY);
        });
      });
    </script>
    
  </body>
</html>
```
### 原理
由于不同浏览器所支持的光标文件格式不尽相同，Opera 和 IE 仅支持 .cur 格式，Firefox、Chrome 和 Safari 既支持 .cur 格式，也支持常见的 .jpg、.gif、.jpg 等格式。
所以从通用性的角度来看，.cur 格式是最保险的，不过也不用担心，如果出现不兼容的情况，系统会选择默认的样式。
作者：刘悦的技术博客
链接：[https://juejin.cn/post/6844904102124584967](https://juejin.cn/post/6844904102124584967)
来源：稀土掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

- **利用 **`**cursor**`** 修改鼠标样式**
```css
cursor: auto;
cursor: pointer;
...
cursor: zoom-out;
/* 使用图片 */
cursor: url(hand.cur)
/* 使用图片，并且设置 fallback 兜底 */
cursor: url(hand.cur), pointer;
```

在不同场景下，选择不同鼠标指针样式，也是一种提升用户体验的手段。
![](https://cdn.nlark.com/yuque/0/2022/webp/533230/1658890610519-c7e5ee8a-9588-497f-94ff-06574066ccd9.webp#averageHue=%23f7f3f2&clientId=uddb4e468-5619-4&from=paste&id=u967b29ac&originHeight=320&originWidth=1352&originalType=url&ratio=1&rotation=0&showTitle=false&status=done&style=none&taskId=u5e67d010-7361-45f4-9a35-0a41c81d0da&title=)

![](https://cdn.nlark.com/yuque/0/2022/webp/533230/1658890615732-1676a8d8-1098-42ee-be0a-f3bd023c5086.webp#averageHue=%23f9f8f8&clientId=uddb4e468-5619-4&from=paste&id=ua1729282&originHeight=362&originWidth=1540&originalType=url&ratio=1&rotation=0&showTitle=false&status=done&style=none&taskId=u0a1392cc-2b4b-48c7-8e7a-2eb1121adbe&title=)

- **实现鼠标指针跟随交互**

1）隐藏鼠标指针，用模拟的指针来替代
```css
 cursor: none;
```

2）通过全局事件监听，模拟鼠标指针
模拟鼠标指针
实现一个 `10px x 10px` 的圆形 div，设置为基于 `<body>` 绝对定位
```html
<div id="g-pointer"></div>
```
```css
#g-pointer {
    position: absolute;
    top: 0;
    left: 0;
    width: 10px;
    height: 10px;
    background: #000;
    border-radius: 50%;
}
```
接着，通过事件监听，监听 body 上的 `mousemove`，将小圆形的位置与实时鼠标指针位置重合：
```javascript
const element = document.getElementById("g-pointer");
const body = document.querySelector("body");

function setPosition(x, y) {
  element.style.transform  = `translate(${x}px, ${y}px)`;                
}

body.addEventListener('mousemove', (e) => {
  window.requestAnimationFrame(function(){
    setPosition(e.clientX - 5, e.clientY - 5);
  });
});
```
在这个基础上，由于现在的鼠标指针，实际上是个 `div`，**因此我们可以给它加上任意的交互效果**。

以文章一开头的例子为例，我们只需要借助混合模式 `mix-blend-mode: exclusion`，就能够实现让模拟的鼠标指针能够智能地在不同背景色下改变自己的颜色。

**伪类事件触发**
有一点需要注意的是，利用模拟的鼠标指针去 **Hover** 元素，**Click** 元素的时候，会发现这些事件都无法触发。
这是由于，此时被隐藏的指针下面，其实悬浮的我们模拟鼠标指针，因此，所有的 Hover、Click 事件都触发在了这个元素之上。
当然，这个也非常好解决，我们只需要给模拟指针的元素，添加上 `pointer-events: none`，阻止默认的鼠标事件，让事件透传即可：
```css
{
    pointer-events: none;
}
```

作者：chokcoco
链接：[https://juejin.cn/post/7111517270899163172](https://juejin.cn/post/7111517270899163172)
来源：稀土掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
_参考阅读：_
[Mouse Cursor Transition](https://link.juejin.cn/?target=https%3A%2F%2Fcodepen.io%2FChokcoco%2Fpen%2FrNJQXXV)
[利用混合模式，让文字智能适配背景颜色](https://github.com/chokcoco/iCSS/issues/169)



---

## 8.鼠标移入显示图片
[鼠标移入显示图片](https://codepen.io/alphardex/pen/OJPmQGz)

---


## 9. CSS3 横向无缝滚动

```html
<div class="position-row justify-center" style="visibility: visible;">
				<div class="hero-marquee">
					<div class="Marquee-tag">designer</div>
					<div class="Marquee-tag">teacher</div>
					<div class="Marquee-tag">facilitator</div>
					<div class="Marquee-tag">speaker</div>
					<div class="Marquee-tag">designer</div>
					<div class="Marquee-tag">teacher</div>
					<div class="Marquee-tag">facilitator</div>
					<div class="Marquee-tag">speaker</div>
					<div class="Marquee-tag">designer</div>
					<div class="Marquee-tag">teacher</div>
					<div class="Marquee-tag">facilitator</div>
					<div class="Marquee-tag">speaker</div>
				</div>
			</div>
```

```css
// https://brutallyhuman.com/

*, *::after, *::before {
    -webkit-box-sizing: border-box;
    box-sizing: border-box;
}
.position-row {
    position: relative;
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
    display: -webkit-box;
    display: -moz-box;
    display: -webkit-flex;
    display: -ms-flexbox;
    display: box;
    display: flex;
    overflow: hidden;
    visibility: hidden;
}
.position-row {
    overflow: hidden;
    margin-top: 5%;
    position: relative;
}
.hero-marquee {
    display: -webkit-box;
    display: -moz-box;
    display: -webkit-flex;
    display: -ms-flexbox;
    display: box;
    display: flex;
    -webkit-animation: marquee-top 22s linear infinite running;
    -moz-animation: marquee-top 22s linear infinite running;
    -o-animation: marquee-top 22s linear infinite running;
    -ms-animation: marquee-top 22s linear infinite running;
    animation: marquee-top 22s linear infinite running;
    position: relative;
    backface-visibility: hidden;
}
.hero-marquee .Marquee-tag {
    width: 18vw;
    display: -webkit-inline-box;
    display: -moz-inline-box;
    display: -webkit-inline-flex;
    display: -ms-inline-flexbox;
    display: inline-box;
    display: inline-flex;
    -webkit-box-align: center;
    -moz-box-align: center;
    -o-box-align: center;
    -ms-flex-align: center;
    -webkit-align-items: center;
    align-items: center;
    -webkit-transition: all 0.2s ease;
    -moz-transition: all 0.2s ease;
    -o-transition: all 0.2s ease;
    -ms-transition: all 0.2s ease;
    transition: all 0.2s ease;
    position: relative;
    justify-content: center;
}
.position-row .Marquee-tag {
    position: relative;
    font-size: 1.302vw;
}
.position-row .Marquee-tag::before {
    content: "";
    left: 0;
    height: 12px;
    width: 12px;
    display: block;
    background-color: var(--second-color);
    border-radius: 100%;
    top: 36%;
    position: absolute;
}

/*--------Hero ribbon Test------*/
@keyframes marquee-top {
    0% {
      -webkit-transform: translateX(0);
      -moz-transform: translateX(0);
      -o-transform: translateX(0);
      -ms-transform: translateX(0);
      transform: translateX(0); 
    }
    100% {
      -webkit-transform: translate(-50%);
      -moz-transform: translate(-50%);
      -o-transform: translate(-50%);
      -ms-transform: translate(-50%);
      transform: translate(-50%);    
    }
  }

```

---

## 10. 优化网页滚动
为网页滚动增加缓动效果，提升浏览体验。但是因为绑定了滚动事件，所以如果存在 返回顶部的 scrollTop 事件，会冲突。
```html
<!-- 在页面载入，或者其他方式触发均可 -->
<body onload="init()"> 
```
```javascript
function init(){
  new SmoothScroll(document,80,16)
}

function SmoothScroll(target, speed, smooth) {
  if (target === document)
    target = (document.scrollingElement 
              || document.documentElement 
              || document.body.parentNode 
              || document.body) // cross browser support for document scrolling
  
  var moving = false
  var pos = target.scrollTop
  var frame = target === document.body 
  && document.documentElement 
  ? document.documentElement 
  : target // safari is the new IE
  
  target.addEventListener('mousewheel', scrolled, { passive: false })
  target.addEventListener('DOMMouseScroll', scrolled, { passive: false })
  
  function scrolled(e) {
    e.preventDefault(); // disable default scrolling
    var delta = normalizeWheelDelta(e)
    pos += -delta * speed
    pos = Math.max(0, Math.min(pos, target.scrollHeight - frame.clientHeight)) // limit scrolling
    if (!moving) update()
  }
  
  function normalizeWheelDelta(e){
    if(e.detail){
      if(e.wheelDelta)
        return e.wheelDelta/e.detail/40 * (e.detail>0 ? 1 : -1) // Opera
      else
        return -e.detail/3 // Firefox
    }else
      return e.wheelDelta/120 // IE,Safari,Chrome
  }
  
  function update() {
    moving = true
    var delta = (pos - target.scrollTop) / smooth
    target.scrollTop += delta
    if (Math.abs(delta) > 0.5)
      requestFrame(update)
    else
      moving = false
  }
  
  var requestFrame = function() { // requestAnimationFrame cross browser
    return (
      window.requestAnimationFrame ||
      window.webkitRequestAnimationFrame ||
      window.mozRequestAnimationFrame ||
      window.oRequestAnimationFrame ||
      window.msRequestAnimationFrame ||
      function(func) {
        window.setTimeout(func, 1000 / 50);
      }
    );
  }()
  }
  
```

---


## 11. hover 跟随显示图片


---

## 12. 原生 JS 实现鼠标滚轮触发页面横向滚动

```html
  <style>
        .box{
            display: flex;
            overflow: scroll;
        }
        .item{
            width: 100vw;
            height: 300vh;
            flex-shrink: 0;
        }
        .item:nth-child(1){
            background-image: linear-gradient(rgb(250, 93, 93), rgb(89, 0, 255));
        }
        .item:nth-child(2){
            background-image: linear-gradient(rgb(240, 250, 150), rgb(104, 170, 255));
        }
        .item:nth-child(3){
            background-image: linear-gradient(rgb(240, 144, 253), rgb(153, 252, 128));
        }
    </style>



    <div class="box">
        <div class="item"></div>
        <div class="item"></div>
        <div class="item"></div>
    </div>



    <script>
        let box = document.querySelector('.box')
        box.addEventListener('wheel', (event)=>{
            event.preventDefault()
            box.scrollLeft += event.deltaY
        })
    </script>

作者：南极一块修炼千年的大冰块
链接：https://juejin.cn/post/6974018969690734628
来源：稀土掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

---

## 13. 文字跑马灯 纯CSS版本

### 版本一：

```css
<div class="c-rail-wrap" style="--scaleY:0;">
		<div class="c-rail -heading u-anim-translate is-inview">
				<div class="c-rail_inner">
						<div class="c-rail_item">
								<span class="c-rail_label">FREE SIGNUP</span>
						</div>
						<div class="c-rail_item">
								<span class="c-rail_label">FREE SIGNUP</span>
						</div>
						<div class="c-rail_item">
								<span class="c-rail_label">FREE SIGNUP</span>
						</div>
						<div class="c-rail_item">
								<span class="c-rail_label">FREE SIGNUP</span>
						</div>                        
						<div class="c-rail_item">
								<span class="c-rail_label">FREE SIGNUP</span>
						</div>
				</div>
				<div class="c-rail_inner">
						<div class="c-rail_item">
								<span class="c-rail_label">FREE SIGNUP</span>
						</div>
						<div class="c-rail_item">
								<span class="c-rail_label">FREE SIGNUP</span>
						</div>
						<div class="c-rail_item">
								<span class="c-rail_label">FREE SIGNUP</span>
						</div>
						<div class="c-rail_item">
								<span class="c-rail_label">FREE SIGNUP</span>
						</div>                        
						<div class="c-rail_item">
								<span class="c-rail_label">FREE SIGNUP</span>
						</div>
				</div>
		</div>
</div>
```
```css
.c-rail-wrap{
    margin:12px auto 0;
}
.c-rail {
    position: relative;
    display: flex;
    align-items: center;
    width: 100%;
    height: auto;
    white-space: nowrap;
    overflow: hidden;
    background-color: #f1f7ff;
}

.c-rail.-heading .c-rail_inner {
    -webkit-animation-duration: 40s !important;
    animation-duration: 40s !important
}


.c-rail_item {
    padding-top:0.25rem;
    padding-bottom: 0.25rem;
    position: relative;
    padding-right: 1.25rem;
    display: flex;
    align-items: center;
    width: auto;
}
.c-rail_item .o-icon{display: none;}
.c-rail_label {
    font-size: 1.5rem;
    padding-right: 2rem;
    font-family: transducer-extended, sans-serif;
    font-weight: 600;
    text-transform: uppercase;
    color: #475d8f;
    text-shadow: none;
}


.c-rail .c-rail_inner {
    display: flex;
    height: 100%;
    -webkit-animation-name: rail;
    animation-name: rail;
    -webkit-animation-duration: 40s !important;
    animation-duration: 40s !important;
    -webkit-animation-play-state: running;
    animation-play-state: running;
    animation-timing-function: linear;
    animation-iteration-count: infinite;
}

@-webkit-keyframes rail {
    0% {
        -webkit-transform: translateZ(0);
        transform: translateZ(0)
    }

    100% {
        -webkit-transform: translate3d(-100%, 0, 0);
        transform: translate3d(-100%, 0, 0)
    }
}

@keyframes rail {
    0% {
        -webkit-transform: translateZ(0);
        transform: translateZ(0)
    }

    100% {
        -webkit-transform: translate3d(-100%, 0, 0);
        transform: translate3d(-100%, 0, 0)
    }
}

.o-icon {
    display: block;
}

.c-rail.-heading .c-rail_item .o-icon {
    margin: 0.675rem 0 0 0;
}

@media (min-width: 64rem) {
    .c-rail.-heading .c-rail_item .o-icon {
        margin: 0.875rem 0 0 0;
    }
}
```
### 版本二：


```html
    <div class="string-scroll" >
        <div class="string-scroll__text">
          START YOUR ROMANTIC JOURNEY! START YOUR ROMANTIC JOURNEY! START YOUR ROMANTIC JOURNEY! START YOUR ROMANTIC JOURNEY! START YOUR ROMANTIC JOURNEY! START YOUR ROMANTIC JOURNEY! START YOUR ROMANTIC JOURNEY! START YOUR ROMANTIC JOURNEY! START YOUR ROMANTIC JOURNEY! START YOUR ROMANTIC JOURNEY! START YOUR ROMANTIC JOURNEY! START YOUR ROMANTIC JOURNEY! 
        </div>
    </div>
```
```css
.string-scroll {
    position: absolute;
    overflow: hidden;
    width: 100%;
    margin: 0 auto;
    white-space: nowrap;
}
.string-scroll__text{
    display: inline-block;
    width: -webkit-max-content;
    width: -moz-max-content;
    width: max-content;
    -webkit-animation: infiniteString 20s linear infinite;
    animation: infiniteString 20s linear infinite;
    letter-spacing: .04em;
    color: #f6c076;
    text-shadow: 0 0 1px rgba(148,32,239,0.5), 0 0 1px rgba(148,32,239,0.5), 0 0 1px rgba(148,32,239,0.5), 0 0 1px rgba(148,32,239,0.5);
    font-size: 29px;
    font-weight: 800;
    line-height: 29px;
}
.infiniteString{
-webkit-animation:infiniteString 10s linear infinite;
animation:infiniteString 10s linear infinite;
}
/* animation */
@-webkit-keyframes infiniteString{0%{-webkit-transform:translate(0);transform:translate(0)}to{-webkit-transform:translate(-25%);transform:translate(-25%)}}
@keyframes infiniteString{0%{-webkit-transform:translate(0);transform:translate(0)}to{-webkit-transform:translate(-25%);transform:translate(-25%)}}
```

---

## 14. marquee 图片左右横向滚动 纯CSS

```css
    <div class="marquee marquee_right" style="background-image:url(https://i.gstatvb.com/0089d2b02baa073ab43ffc16b862408d1650618846.rng.png)"></div>
```

```css
.marquee {
  width: 100vw;
  height: 232px;
  -webkit-animation: 400s linear infinite;
  animation: 400s linear infinite;
  background: bottom/auto 100% repeat-x
}

.marquee_left {
  -webkit-animation-name: slide-left;
  animation-name: slide-left
}

.marquee_right {
  -webkit-animation-name: slide-right;
  animation-name: slide-right
}

@-webkit-keyframes slide-left {
  0% {
      background-position-x: 0
  }

  to {
      background-position-x: 1000vw
  }
}

@keyframes slide-left {
  0% {
      background-position-x: 0
  }

  to {
      background-position-x: 1000vw
  }
}

@-webkit-keyframes slide-right {
  0% {
      background-position-x: 0
  }

  to {
      background-position-x: -1000vw
  }
}

@keyframes slide-right {
  0% {
      background-position-x: 0
  }

  to {
      background-position-x: -1000vw
  }
}

@media only screen and (max-width:540px) {
  .marquee {
      height: 164px;
      -webkit-animation-duration: 200s;
      animation-duration: 200s
  }
}
```

---

## 15. 动态手绘线条


![image.png](https://cdn.nlark.com/yuque/0/2022/png/533230/1672045585163-056b42b1-a58f-440e-87af-29d016b567b6.png#averageHue=%23c3d4e7&clientId=u710765bc-c0ad-4&from=paste&height=82&id=ua744b771&name=image.png&originHeight=82&originWidth=380&originalType=binary&ratio=1&rotation=0&showTitle=false&size=11641&status=done&style=none&taskId=ua0b21dd8-bcc3-4726-8cc7-ffcc35249d9&title=&width=380)

```html
<span class="dnxt-text-highlight-animated-wrapper">
	<span class="dnxt-text-highlight dnxt-text-highlight-animated-text">Eastern Europe!</span>
	<span>
		<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 500 150" preserveAspectRatio="none"><path d="M7.7,145.6C109,125,299.9,116.2,401,121.3c42.1,2.2,87.6,11.8,87.3,25.7"></path></svg></span>
</span>
```
```css
svg:not(:root) {
	overflow: hidden;
}

.dnxt-text-highlight-animated-wrapper {
	overflow: visible;
	position: relative
}

.dnxt-text-highlight-animated-text {
	z-index: 1;
	position: relative
}

.dnxt-text-highlight-animated-wrapper svg {
	position: absolute;
	top: 50%;
	left: 50%;
	width: calc(100% + 20px);
	height: calc(100% + 20px);
	-webkit-transform: translate(-50%, -50%);
	transform: translate(-50%, -50%);
	overflow: visible
}

.dnxt-text-highlight-animated-wrapper path {
	stroke-linecap: round;
	stroke-linejoin: round
}
.dnxt-text-highlight-animated-wrapper svg path {
	fill: none;
	stroke-dasharray: 1500;
	stroke-dashoffset: 1500;
	-webkit-animation: dnxt-text-highlight-headline-dash 10s infinite;
	animation: dnxt-text-highlight-headline-dash 10s infinite;
	stroke-width: 17px;
	stroke: #470fdd;
	-webkit-animation-delay: 1000ms;
	animation-delay: 1000ms;
}

@-webkit-keyframes dnxt-text-highlight-headline-dash {
	0% {
	stroke-dashoffset: 1500
}

15% {
stroke-dashoffset: 0
}

85% {
	opacity: 1
}

90% {
stroke-dashoffset: 0;
opacity: 0
}

to {
	stroke-dashoffset: 1500;
	opacity: 0
}
}

@keyframes dnxt-text-highlight-headline-dash {
	0% {
		stroke-dashoffset: 1500
	}

	15% {
		stroke-dashoffset: 0
	}

	85% {
		opacity: 1
	}

	90% {
		stroke-dashoffset: 0;
		opacity: 0
	}

	to {
		stroke-dashoffset: 1500;
		opacity: 0
	}
}

```

---

## 16. css animation 实现颜色渐变动画
3种颜色和五种颜色循环变换
配合 blur 属性使用。
```html
   <div class="light-ellipse light-ellipse--right color-change-3x"></div>
```
```html
* {
    box-sizing: border-box;
    outline: none;
}
.light-ellipse {
    position: relative;
    top: 0;
    left:0;
    text-align: center;
    background: #5f7d95;
    opacity: 0.7;
    -webkit-filter: blur(170px);
    filter: blur(170px);
    width: 640px;
    height: 410px;
    z-index: -1;
    display:block;
}
.light-ellipse--right {
    -webkit-backface-visibility: hidden;
    -moz-backface-visibility: hidden;
    -webkit-transform: translate3d(0, 0, 0);
    -moz-transform: translate3d(0, 0, 0);
}
:root{
    --colorStart: #10a3a8;
    --colorSecond: #7c32db;
    --colorThird: #ff004e
}

.color-change-3x {
    -webkit-animation: color-change-3x 9s linear infinite normal;
    animation: color-change-3x 9s linear infinite normal
}

@-webkit-keyframes color-change-3x {
    0% {
        background: var(--colorStart)
    }

    33% {
        background: var(--colorSecond)
    }

    66% {
        background: var(--colorThird)
    }

    100% {
        background: var(--colorStart)
    }
}

@keyframes color-change-5x {
    0% {
        background: var(--colorStart)
    }

    33% {
        background: var(--colorSecond)
    }

    66% {
        background: var(--colorThird)
    }

    100% {
        background: var(--colorStart)
    }
}

.color-change-5x {
    -webkit-animation: color-change-5x 9s linear infinite normal;
    animation: color-change-5x 9s linear infinite normal
}

@-webkit-keyframes color-change-5x {
    0% {
        background: var(--colorStart);
        left: var(--leftStart);
        top: var(--topStart)
    }

    20% {
        background: var(--colorSecond);
        left: var(--leftStart);
        top: var(--topEnd)
    }

    40% {
        background: var(--colorThird);
        left: var(--leftEnd);
        top: var(--topStart)
    }

    60% {
        background: var(--colorFourth);
        left: var(--leftEnd);
        top: var(--topStart)
    }

    80% {
        background: var(--colorEnd);
        left: var(--leftEnd);
        top: var(--topEnd)
    }

    100% {
        background: var(--colorStart);
        left: var(--leftStart);
        top: var(--topStart)
    }
}

@keyframes color-change-5x {
    0% {
        background: var(--colorStart);
        left: var(--leftStart);
        top: var(--topStart)
    }

    20% {
        background: var(--colorSecond);
        left: var(--leftStart);
        top: var(--topEnd)
    }

    40% {
        background: var(--colorThird);
        left: var(--leftEnd);
        top: var(--topStart)
    }

    60% {
        background: var(--colorFourth);
        left: var(--leftEnd);
        top: var(--topStart)
    }

    80% {
        background: var(--colorEnd);
        left: var(--leftEnd);
        top: var(--topEnd)
    }

    100% {
        background: var(--colorStart);
        left: var(--leftStart);
        top: var(--topStart)
    }
}

```

---

## 

---

## 17. 数值范围随机增减 - 原生JS 
```javascript
function randomNum(){
  let num=document.getElementById("num");
  var timeRun = 0;
  let myTime = setInterval(function(){
    num.innerText = 2137 + Math.round(Math.random() * 100);
    timeRun +=1;
    if(timeRun === 5){
      clearInterval(myTime)
    }
  },100)
}
setInterval(function(){
  randomNum();
},5000)
randomNum();
```





# 知识学习

使用案例来深化
