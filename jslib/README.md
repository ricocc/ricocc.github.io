# Js library


# 一些零零散散的代码速记

# 代码块



### 1. 前端JS无缝滚动

工作中网页会有特定场景需要用到滚动的需求，记录一下最后选择的方式

参考文章： [前端js无缝滚动---解决两个小bug]( https://blog.csdn.net/qq_34831149/article/details/86678848)

目前应用到的页面是  [ukrainebeauty.net/12](https://www.ukrainebeauty.net/qa/register12.php)  和  [ukrainebeauty.net/14](https://www.ukrainebeauty.net/qa/register14.php)

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



### 2. 模拟在线人数自动变化



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



### 3. 鼠标移动位移

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



### 4. 倒计时

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





### 5. 滚动加载

```html
class="revealOnScroll ani animated" data-animation="ani" data-timeout="50"
```



```js
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

### 6. 判断移动端设备

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

### 7. 修改鼠标指针 cursor 

参考阅读：

[有意思的鼠标指针交互探究](https://juejin.cn/post/7111517270899163172)



由于不同浏览器所支持的光标文件格式不尽相同，Opera 和 IE 仅支持 .cur 格式，Firefox、Chrome 和 Safari 既支持 .cur 格式，也支持常见的 .jpg、.gif、.jpg 等格式。

所以从通用性的角度来看，.cur 格式是最保险的，不过也不用担心，如果出现不兼容的情况，系统会选择默认的样式。

作者：刘悦的技术博客
链接：https://juejin.cn/post/6844904102124584967
来源：稀土掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。



利用 `cursor` 修改鼠标样式

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

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5808772bc55b48fdbc56abbfd84e6950~tplv-k3u1fbpfcp-zoom-in-crop-mark:3024:0:0:0.awebp)

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5761bb1d7af3499390bb0a0fd483aeec~tplv-k3u1fbpfcp-zoom-in-crop-mark:3024:0:0:0.awebp)





**实现鼠标指针跟随交互**

1）隐藏鼠标指针，用模拟的指针来替代

```
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

伪类事件触发

有一点需要注意的是，利用模拟的鼠标指针去 **Hover** 元素，**Click** 元素的时候，会发现这些事件都无法触发。

这是由于，此时被隐藏的指针下面，其实悬浮的我们模拟鼠标指针，因此，所有的 Hover、Click 事件都触发在了这个元素之上。

当然，这个也非常好解决，我们只需要给模拟指针的元素，添加上 `pointer-events: none`，阻止默认的鼠标事件，让事件透传即可：

```css
{
    pointer-events: none;
}
```



作者：chokcoco
链接：https://juejin.cn/post/7111517270899163172
来源：稀土掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

*参考阅读：*

[Mouse Cursor Transition](https://link.juejin.cn/?target=https%3A%2F%2Fcodepen.io%2FChokcoco%2Fpen%2FrNJQXXV)

[利用混合模式，让文字智能适配背景颜色](https://github.com/chokcoco/iCSS/issues/169)

---

### 8. 鼠标移入显示图片

[鼠标移入显示图片](https://codepen.io/alphardex/pen/OJPmQGz)



---

### 9. CSS3 横向无缝滚动



```html
            <div class="c-rail-wrap" style="--scaleY:0;">
                <div class="c-rail -heading u-anim-translate is-inview">
                    <div class="c-rail_inner">
                        <div class="c-rail_item"><span class="c-rail_label">FREE SIGNUP</span>
                            <div class="o-icon"><svg class="svg-smile">
                                    <use xlink:href="img/sprite.svg#svg-smile"></use>
                                </svg></div>
                        </div>
                        <div class="c-rail_item"><span class="c-rail_label">FREE SIGNUP</span>
                        </div>
                        <div class="c-rail_item"><span class="c-rail_label">FREE SIGNUP</span>
                        </div>
                    </div>
                    <div class="c-rail_inner">
                        <div class="c-rail_item"><span class="c-rail_label">FREE SIGNUP</span>
                        </div>
                        <div class="c-rail_item"><span class="c-rail_label">FREE SIGNUP</span>
                        </div>
                        <div class="c-rail_item"><span class="c-rail_label">FREE SIGNUP</span>
                        </div>
                    </div>
                </div>
            </div>
```



CSS 

```css
.c-rail-wrap{
    margin:36px auto 0;
}
.c-rail {
    position: relative;
    display: flex;
    align-items: center;
    width: 100%;
    height: auto;
    white-space: nowrap;
    overflow: hidden;
    background-color: #f0f0f0;
    box-sizing: border-box;
    padding:0.5rem 0;
}

.c-rail.-heading .c-rail_inner {
    -webkit-animation-duration: 40s !important;
    animation-duration: 40s !important
}


.c-rail_item {
    position: relative;
    padding-right: 2rem;
    display: flex;
    align-items: center;
    width: auto;
}
.c-rail_item .o-icon{display: none;}
.c-rail_label {
    font-size: 1.5rem;
    padding-right: 0rem;
    font-family: transducer-extended, sans-serif;
    font-weight: 600;
    text-transform: uppercase;
    color: #5193dc;
    text-shadow: none;
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
```



### 10. 优化网页滚动

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



### 11. hover 显示图片

https://codepen.io/alphardex/pen/OJPmQGz







### 12. CSS 飘爱心

```html
<div class="heartsbox">
  <div style="width:100%;margin:0 auto;">
    <div class="heart-container"><div class="heart anim1">♥</div></div>
    <div class="heart-container"><div class="heart anim2">♥</div></div>
    <div class="heart-container"><div class="heart anim3">♥</div></div>
    <div class="heart-container"><div class="heart anim4">♥</div></div>
    <div class="heart-container"><div class="heart anim1">♥</div></div>
    <div class="heart-container"><div class="heart anim2">♥</div></div>
    <div class="heart-container"><div class="heart anim3">♥</div></div>
    <div class="heart-container"><div class="heart anim4">♥</div></div>
    <div class="heart-container"><div class="heart anim1">♥</div></div>
    <div class="heart-container"><div class="heart anim2">♥</div></div>
  </div>
</div>
<style>
.heartsbox{
  position:fixed;
  width:90%;
  bottom:-50px;
  left:5%;
  z-index:1
}

.heart{
  color:#fdf5e6;
  font-size:25px;
  position:absolute;
  bottom:0;
  right:50px;
  animation-name:movement;
  animation-duration:4s;
  animation-timing-function:linear;
  animation-iteration-count:infinite}

.heart-container {
    margin-top: 20px;
    width: 10%;
    height: 50%;
    text-align: center;
    position: relative;
    display: inline-block;
    float: left;
}
.anim1{
  animation-delay:1s}
.anim2{
  animation-delay:1.5s}
.anim3{
  animation-delay:.5s}
.anim4{
  animation-delay:1.9s}
@keyframes movement{
  0%{
    bottom:0;
    right:50px}
  20%{
    color:#ff69b4;
    right:40px}
  40%{
    right:60px}
  50%{
    right:50px}
  60%{
    right:40px}
  70%{
    right:50px}
  80%{
    right:45px}
  90%{
    right:50px}
  100%{
    bottom:600px;
    -webkit-opacity:0;
    -moz-opacity:0;
    opacity:0}
}
</style>
```



### 13. 数值限定范围随机增减

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



# 插件库



### 1. 插件库 -  JParticles 随机粒子运动

同样也是这两个页面背景运用到的粒子效果插件  [ukrainebeauty.net/12](https://www.ukrainebeauty.net/qa/register12.php)  和  [ukrainebeauty.net/14](https://www.ukrainebeauty.net/qa/register14.php) 

粒子插件：[**JParticles - 一个简洁，高效，轻量级的 Canvas 粒子运动特效库**](https://jparticles.js.org/)

使用简单，轻量级，可设置参数多。

具体看文档就已经够详细了。

目前具体效果有五个，分别是：

- 粒子运动（Particle）
- 波纹运动（Wave）
- 波纹进度条（WaveLoading）
- 雪花飘落（Snow）
- 线条动画（Line）

在具体的场景设计上面，可以起到不错的效果。



### 2. Swiper 轮播插件

[Swiper 中文网](https://www.swiper.com.cn/)



### 3. ScrollTrigger 页面滚动触发 `HTML` 元素动画

说明链接： 

[膜拜！用最少的代码却实现了最牛逼的滚动动画！](https://juejin.cn/post/7038378577028448293)  

[GSAP 动画插件 - ScrollTrigger（一）](https://zhuanlan.zhihu.com/p/346555713)

`ScrollTrigger` 是基于 `GSAP` 实现的一款高性能页面滚动触发 `HTML` 元素动画的插件。

通过 `ScrollTrigger` 使用最少的代码创建令人叹为观止的滚动动画。我们需要知道 `ScrollTrigger` 是基于 `GSAP` 实现的插件，`ScrollTrigger` 是处理滚动事件的，而真正处理动画是 `GSAP`，二者组合使用才能实现滚动动画～








