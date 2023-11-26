### 一、字体与兼容性

**1. TureTpe(.ttf)格式：**
.ttf字体是Windows和Mac的最常见的字体，是一种RAW格式，因此他不为网站优化,支持这种字体的浏览器有【IE9+,Firefox3.5+,Chrome4+,Safari3+,Opera10+,iOS Mobile Safari4.2+】；

**2. OpenType(.otf)格式：**
.otf字体被认为是一种原始的字体格式，其内置在TureType的基础上，所以也提供了更多的功能,支持这种字体的浏览器有【Firefox3.5+,Chrome4.0+,Safari3.1+,Opera10.0+,iOS
Mobile Safari4.2+】；

**3. Web Open Font Format(.woff)格式：**
**.woff字体是Web字体中最佳格式**，他是一个开放的TrueType/OpenType的压缩版本，同时也支持元数据包的分离,支持这种字体的浏览器有【IE9+,Firefox3.5+,Chrome6+,Safari3.6+,Opera11.1+】；

**4. Embedded Open Type(.eot)格式：**
.eot字体是**IE专用字体**，可以从TrueType创建此格式字体,支持这种字体的浏览器有【IE4+】；

**5. SVG(.svg)格式：**
.svg字体是基于SVG字体渲染的一种格式,支持这种字体的浏览器有【Chrome4+,Safari3.1+,Opera10.0+,iOS Mobile Safari3.2+】。

### 二、@font-face
```css
  @font-face {
    font-family: 'YourWebFontName';
    src: url('YourWebFontName.eot?#iefix') format('eot');/*IE*/
    src:url('YourWebFontName.woff') format('woff'), url('YourWebFontName.ttf') format('truetype');/*non-IE*/
   }
```
但为了让各多的浏览器支持，你也可以写成：
```css
   @font-face {
    font-family: 'YourWebFontName';
    src: url('YourWebFontName.eot'); /* IE9 Compat Modes */
    src: url('YourWebFontName.eot?#iefix') format('embedded-opentype'), /* IE6-IE8 */
             url('YourWebFontName.woff') format('woff'), /* Modern Browsers */
             url('YourWebFontName.ttf')  format('truetype'), /* Safari, Android, iOS */
             url('YourWebFontName.svg#YourWebFontName') format('svg'); /* Legacy iOS */
   }
```
### 
### 三、获取字体途径
[https://www.fontsquirrel.com/](https://link.jianshu.com?t=https://www.fontsquirrel.com/)
### 四、转换字体格式
首推：
[https://cloudconvert.com/](https://cloudconvert.com/)

[https://convertio.co/zh/font-converter/](https://convertio.co/zh/font-converter/)
[http://www.freefontconverter.com/](https://link.jianshu.com?t=http://www.freefontconverter.com/)
[http://font2web.com/](https://link.jianshu.com?t=http://font2web.com/)
[http://www.youziku.com/](https://link.jianshu.com?t=http://www.youziku.com/)

### 五、中文字体
因为中文字体比较大，要用其他方法才能实现，可以参考有字网。
### 参考文章：
[http://www.phpvar.com/archives/2663.html](https://link.jianshu.com?t=http://www.phpvar.com/archives/2663.html)
[http://www.w3cplus.com/content/css3-font-face](https://link.jianshu.com?t=http://www.w3cplus.com/content/css3-font-face)
https://www.jianshu.com/p/fda434dbd336
### 扩展
[图标字体](https://link.jianshu.com?t=https://isux.tencent.com/icon-font.html)

