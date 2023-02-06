# AE 学习

## 知识


- bodymovin插件 和 lottie-web
[[笔记]从AE动画到web代码](https://juejin.cn/post/6977523390412226573#heading-2)


- 基础教程
  [拜托三连了！这绝对是全B站最用心（没有之一）的AE公开课程，耗时千余小时开发!](https://www.bilibili.com/video/BV1ZA411g7Sb?p=11)

  

## 常用插件

- 湍流置换效果

  [湍流置换效果插件教学](https://www.bilibili.com/video/BV1ZA411g7Sb?p=6)

  

- Soft Body - AE快速模拟柔体碰撞效果
  [用AE快速模拟柔体碰撞效果——Soft Body](https://www.bilibili.com/video/BV1RK411g7pQ/?spm_id_from=333.788.recommend_more_video.0)

  

- 三维场景神器 v1.0.2

[三维场景神器 v1.0.2](https://www.bilibili.com/video/BV1yK4y157rs?spm_id_from=333.999.0.0)



## 常用表达式 

> 动画建议通过建立空对象绑定进行控制



### wiggle(频率,振幅)	抖动

**wiggle(2，30)		频率就是单位时间内震动的次数，振幅就是震动的幅度**

过赋予物体随机值使之实现随机摆动，它确实能让你得到你想象中的效果。这个表达式可以让你的动效看起来更加生动和自然。表达式中的第一个数字代表每秒抖动的次数，第二个数字则代表抖动的像素。所以在位置的参数中加入表达式wiggle(2，30)就意味着每秒抖动2次，每次抖动30个像素。



### time*n	时间表达式

**time10	 time 可以提取当前时间的值（第几秒）赋予所给属性，timen就是现在的时间（第几秒）乘以n，用于控制数值变化大小的单调递增函数。**

时间表达式是做循环动画的利器。例如，如果你想让一个物体不停地旋转，你可以在旋转参数中输入time，物体就会每秒转动一度。time表达式同样可以配合基本数学公式使用，如果你想你的物体转动速度是之前的30倍，你可以输入time*30



### Time Remap*n	抽帧表达式

对图层/合成添加时间重映射，然后添加此表达式即可看到效果



### loopOut()	创建循环动画表达式

loopOut()

loopOut表达式同样可以帮我们创建循环动画。然而，与wiggle和时间表达式不同，loopOut表达式需要预先设定关键帧。所以，如果你想让一个物体以一秒为周期旋转一圈，你可以为它添加loopOut表达式，之后它就会永无止境地重复。

loopOut() 括号里面是可以填写内容的，内容如下：

**loopOut(type="类型",numKeyframes=0)**

0表示从第零帧开始循环，循环类型有：

A:cycle：周而复始来回运动

B:offset：叠加之前关键帧循环

C:continue：延续属性变化的最后速度



### Random(x,y)	随机数表达式

区别wiggle（振幅，频率），括号里面两个参数含义，wiggle的是两个控制不同属性的参数，Random中x表示最小值（Min）y表示最大值（Max），表示在最小值和最大值之间随机取一个数字。



### seedRandom(n)

seedRandom(5)

seedRandom虽然只是可以让之前的关键帧变得更丰富，但是当你仔细思考，你会发现它的其它用处。

随机数在AE里并不能完全随机。当然，它可以被称为\"随机\"，但是实际的随机值并不能在javascript中得到，因此AE中也无法得到。正因为这样，我们需要给这些随机一个开始的值。After Effects会自动使用图层在时间线左侧上的数字去作为一个初始值。每一个随机运动的迭代都有一个值，被称为\"seed\"，所以random seed 为1 的运动与random seed 为2 的运动是完全不同的。你可以在你的wiggle表达式前添加一个seedRandom(5)，那它们的随机运动状态就会一摸一样。

如果你改变图层顺序，random seed也会跟着改变，因此你的随机抖动效果也会发生变化。这不是一个大问题，但是有的时候当你有一个看起来几乎完美的随机抖动，你并不会想让它再改变。解决这个问题，你需要使用seedRandom()表达式。这个表达式会帮你锁定随机值，即使改变图层顺序，你的随机运动也不会发生变化。



### Math.round()	取整表达式

Math.round()

Math.round() 是一个可以将小数化整的表达式。这对做倒计时或计时动画来说是一个利器。简单地将你的表达式加入到Math.round()括号之中，你的数字将会化为整数。



### valueAtTime(time-n)	延迟表达式

n表示你想延迟的时间长短

这个表达式可以得到当前时间图层效果的值，并且通过括号内参数对图层效果时间轴往前或往后推移，可制作延迟效果。



### index	图层序号表达式



### Math.sin	表达式

Math方法可以调用ae内部的数学函数，Math相当于一个“盒子”，通过这个“盒子”能够调用ae里面的一些数学运算表达式，例如：sin，Cos等等

举例：Math.sin(time*3)\*times 60

结合sin函数特性，括号内time*3无论取何值，sin() 取值范围在【-1，1】之间
