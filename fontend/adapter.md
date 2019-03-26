###  移动端适配

#### HTML篇

1  采用淘宝移动端适配方案

    JS引入flexible资源

[flexible.debug.js](/uploads/5aea60475f3b331882fbe252a88fdfd8/flexible.debug.js)
[flexible.debug.css](/uploads/ee59954dea58fd9aefe8087b477741a7/flexible.debug.css)

```
import '../assets/js/flexible.debug.js';
import '../assets/css/flexible.debug.css';

```


2  viewport设置

页面中增加默认viewport设置

```
<!-- 让页面宽度等于设备宽度，缩放比例为1，禁止用户缩放网页，适配Iphonex全屏 -->
<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no viewport-fit=cover">
<!-- 设置Web应用是否以全屏模式运行 -->
<meta name="apple-mobile-web-app-capable" content="yes">
<!-- 设置状态栏（屏幕顶部栏）的样式，default为白色，black为黑色，black-translucent为透明 -->
<meta name="apple-mobile-web-app-status-bar-style" content="default">
<!-- 设置添加到主屏幕后的图标 -->
<link rel="apple-touch-icon" href="xxx.png">

```

3   忽略数字默认为电话号码或者邮箱

```
<!-- 忽略网页自动识别数字为电话号码 -->
<meta name="format-detection" content="telephone=no">
<!-- 忽略网页自动识别邮箱账号 -->
<meta name="format-detection" content="email=no">

```

4   调用系统应用

```
<!-- 拨号 -->
<a href="tel:10086">打电话给: 10086</a>
<!-- 短信 -->
<a href="sms:10086">发短信给: 10086</a>
<!-- 邮件 -->
<a href="mailto:839626987@qq.com">发邮件给：839626987@qq.com</a>
<!-- 选择照片或者拍摄照片 -->
<input type="file" accept="image/*">
<!-- 选择视频或者拍摄视频 -->
<input type="file" accept="video/*">
<!-- 多选 -->
<input type="file" multiple>

```

#### CSS篇(提供统一CSS文件引用)

1  字体设置

body元素中增加默认字体设置如下：

```
 font-family: 'PingFang  SC', 'Microsoft YaHei', Arial, sans-serif;

```


2  初始化浏览器内外边距

```
body,
div,
dl,
dt,
dd,
ul,
ol,
li,
h1,
h2,
h3,
h4,
h5,
h6,
pre,
code,
form,
fieldset,
legend,
input,
textarea,
p,
blockquote,
th,
td,
hr,
button,
article,
aside,
details,
figcaption,
figure,
footer,
header,
hgroup,
menu,
nav,
section {
  margin: 0;
  padding: 0;
}

```
3 设置表单元素输入框宽度和字体大小继承父元素

```
input,
select,
textarea {
  font-size: 100%;
  width: 100%;
}

```
4  使用table时，边框去重

```
/* 去掉各 Table  cell 的边距并让其边重合 */
table {
  border-collapse: collapse;
  border-spacing: 0;
}
```

5  去除某些区域点击的时候会出现阴影

```
a, button, input, img, select, textarea,div {
   -webkit-tap-highlight-color: transparent
}
```

6   旋转屏幕时字体大小不改变

```
html, body{
 -webkit-text-size-adjust: 100%;
 -ms-text-size-adjust: 100%;
 text-size-adjust: 100%
}

```

7  box-sizing(盒模型)

使用盒模型时必须指定box-sizing属性为border-box : padding和border被包含在定义的width和height之内

```
div{
   box-sizing: border-box
}

```

8  字数过多，超过父元素宽度，使用...

```
.类名 {
  white-space:nowrap;
  overflow:hidden;
  text-overflow:ellipsis;
}

```

9  使用flex布局，兼容android低版本

```
.类名{
    display: -webkit-box;
    display: -webkit-flex;
    display: -ms-flexbox;
    display: flex;
    // 垂直布局
    -webkit-box-orient: vertical;
    -webkit-box-direction: normal;
    -webkit-flex-direction: column;
    -ms-flex-direction: column;
    flex-direction: column;
 // 垂直居中
    -webkit-box-align: center;
    -webkit-align-items: center;
    -ms-flex-align: center;
    align-items: center;
// 水平居中
    -webkit-box-pack: center;
    -webkit-justify-content: center;
    -ms-flex-pack: center;
    justify-content: center;
}

```
10  input输入框取消默认样式

```
     input{
          -webkit-appearance: none; 
          -moz-appearance: none; 
          -o-appearance: none; 
          appearance: none;
          background:none;
          outline:none;
          border:0px;
    }
```

11  取消列表默认样式

```
/* 去掉列表前的标识, li 会继承 */
ol,
ul {
  list-style: none;
}

```

12  0.5px分割线

 ```
.类名::after{
    content: '';
    position:absolute;  (.类名要提前设置position)
    top:根据定位设置;
    left:根据定位设置;
    height:根据需求稿2倍设置；
    width: 根据需求稿2倍设置；
    transform：scale(.5);
    transform-origin: 0 0;
}

````

13  H5监听屏幕旋转事件并且处理样式

```
/* 竖屏时样式 */
@media all and (orientation:portrait) {
  body::after {
      content: '竖屏'
    }
}
/* 横屏时样式 */
@media all and (orientation:landscape) {
    body::after {
      content: '横屏'
    }
}

```

#### JS篇

1   IE下,event对象有x,y属性,但是没有pageX,pageY属性;Firefox下,event对象有pageX,pageY属性,但是没有x,y属性。
   
```
   //解决方案：
   var page = {};
   page.x = event.x ? event.x : event.pageX;
   page.y = event.y ? event.y:event.pageY;

```

2   事件穿透
点击穿透问题：点击蒙层(mask)上的关闭按钮，蒙层消失后发现触发了按钮下面元素的click事件，解决办法:

* 只用touch
* 只用click
* touch延迟350ms再隐藏蒙层(mask)
* fastclick.js