# 前端面试常见问题以及答案（简洁版）

## 项目介绍
该项目用来覆盖常见的前端面试问题，使用中文和Markdown来完成项目的制作。市面上已经有很多类似的项目了，但是问题和答案都非常的冗长，该项目力求使用简洁的文字来回答面试官所问到的常见问题，希望对您的前端面试有所帮助。

## 目录结构
- [请说说你对闭包的理解？](#说说你对闭包的理解)
- [请解释下浮动问题以及相应的解决方案？](#请解释下浮动问题以及相应的解决方案)
- [如何使用CSS实现文字截断效果？](#如何使用CSS实现文字截断效果)
- [如何使用CSS实现文字居中效果？](#如何使用CSS实现文字居中效果)
- [请说说你对BFC的理解以及相应的使用场景？](#请说说你对BFC的理解以及相应的使用场景)
- [请说说你对响应式布局的理解以及如何实现？](#请说说你对响应式布局的理解以及如何实现)
- [ES2017中async和await关键字有什么作用？](#ES2017中async和await关键字有什么作用)
- [请举例说说网站优化的方法有哪些？](#请举例说说网站优化的方法有哪些)
- [请说说你对前端模块化编程的理解？](#请说说你对前端模块化编程的理解)
- [Git常规操作当中的reset, rebase, revert, merge, fetch在哪些时候会被用到以及它们的不同之处？](#Git常规操作当中的reset-rebase-revert-merge-fetch在哪些时候会被用到以及它们的不同之处)
- [请说说你对虚拟DOM的理解？](#请说说你对虚拟DOM的理解)
- [节流(throttle), 防抖(debounce), 函数柯里化(currying)在实际工程中有什么作用并且简述下其原理？](#节流throttle-防抖debounce-函数柯里化currying在实际工程中有什么作用并且简述下其原理)
- [说说你对跨域问题的理解？](#说说你对跨域问题的理解)
- [常见的网站攻击有哪些，如何通过编码做到相应的防护？](#常见的网站攻击有哪些如何通过编码做到相应的防护)

## 说说你对闭包的理解?
概念：延长嵌套函数中内部函数的作用域到外部函数的组合被称为闭包，当嵌套函数的外部函数被执行完成后，内部函数依旧可以访问外部函数中的变量。其实质是延长了函数的作用域链。

用途：
1. 模仿块级作用域
2. 存储变量
3. 封装私有变量

优点：避免变量污染全局作用域。  
缺点：闭包变量常驻于内存当中，会增大内存的使用量，使用不当容易造成内存泄露。

**[⬆ 回到顶部](#目录结构)**

## 请解释下浮动问题以及相应的解决方案？
在使用CSS布局样式时，当某个元素使用了浮动属性（`float:left/right;`），会导致两个问题：  
1. 与浮动元素同级的非浮动元素会跟随其后
2. 父元素的高度无法被撑开，影响总体展示效果

清除浮动（`clearfix`）的几种方式：
1. 推荐方式
```
.clearfix:before, .clearfix:after {
  content: "";
  display: table;
}

.clearfix:after {
  clear: both;
}
```
2. 使用`:after`伪元素
```
.container:after {
  content: "";
  height: 0;
  visibility: hidden;
  display: block;
  clear: both;
}
```
3. 使用额外的标签（不推荐）
```
<div style="clear:both;"></div>
```

**[⬆ 回到顶部](#目录结构)**

## 请说说你对BFC的理解以及相应的使用场景？
BFC是（Block Formatting Context）的缩写，被称作“块级格式化上下文”，用于实现将某个元素的样式独立于其之前和之后的元素。通俗来说，可以将BFC容器理解为一个封闭的大箱子，箱子内的元素无论如何操作都不会影响到外部元素。

常见的创建BFC容器的两种方式：
1. 使用 `overflow:auto/hidden;` 属性触发BFC特性。
2. 使用 `display:flow-root;` 属性触发BFC，但目前浏览器支持还不是很好。

应用场景及修复问题:
1. 修复外边距折叠问题（Margin Collapsing）。
2. 清除浮动：  
  2.1 限制内部浮动，防止父容器塌陷。  
  2.2 阻止外部浮动，防止子元素中之前的元素遮挡后面的元素。

**[⬆ 回到顶部](#目录结构)**

## 如何使用CSS实现文字截断效果？
1. 单行文字截断：
```
.truncate-single-line {
  white-space: nowrap;     /* 文字不换行 */
  overflow: hidden;        /* 文字超出容器隐藏内容 */
  text-overflow: ellipsis; /* 使用省略号显示文字 */
}
```
2. 多行文字截断
```
.truncate-multi-lines {
  display: -webkit-box;         /* 使用-webkit-box布局显示 */
  -webkit-line-clamp: 3;        /* 显示的行数 */
  -webkit-box-orient: vertical; /* 垂直方向显示内容 */
}
```

**[⬆ 回到顶部](#目录结构)**

## 如何使用CSS实现文字居中效果？
1. 设置单行元素居中  

1.1 实现：设置父元素的高度和行高保持一致
```
.div {
  width: 200px;

  /* 关键代码 */
  height: 200px;
  line-height: 200px;
  text-align: center;
}
```
1.2 实现：设置父元素`display:table-cell;`或者使用`table标签`来实现
```
.div {
  display: table-cell;
}
```
1.3 实现：使用`相对定位`或者`transform`实现
```
.parent {
  position: relative;
}
.use-transform {
  positive: absolute;
  transform: translate(-50%, -50%);
}
```
1.4 实现：通过父元素flex布局属性实现(这些属性同样可以居中多行元素)
```
.parent {
  display: flex;
  align-items: center;    /* 垂直居中 */
  justify-conent: center; /* 水平居中 */
}
```
1.5 实现：使用父元素grid布局属性实现(只能单行)
```
.parent {
  display: grid;
  place-items: center;
}
```

2. 设置多行元素居中  

2.1 实现：使用伪类元素`height:100%; vertical-align:middle;`撑起行高，其他子元素也设置`vertical-align:middle;`
```
.parent {
  width: 200px;
  height: 200px;
  text-align: center;
}
.parent .first-child,
.parent .second-child,
.parent .third-child {
  display: inline-block;

  /* 关键代码 */
  vertical-align: middle;
}
/* 关键代码 */
.parent::before {
  content: "";
  width: 0;
  height: 100%;
  vertical-align: middle;
  positive: relative;
  display: inline-block;
}
```
2.2 实现：通过`相对绝对定位`配合`top, margin-left, calc`等属性进行实现

**[⬆ 回到顶部](#目录结构)**

## 请说说你对响应式布局的理解以及如何实现？
响应式布局的本质是让写出的前端布局代码（`HTML`/`CSS`）可以完美的运行在不同设备上，包括PC、iPad、平板电脑、手机移动设备等，而不出现显示内容走样或者不协调的问题。

具体的做法通常有以下几种：
1. 使用媒体查询（Media Query）。
2. 使用CSS `rem` 像素单位，当不同设备浏览器的尺寸宽度变窄时，动态调节html根元素字体的大小，以实现样式的动态适配。
3. PC端和平板电脑端采用一套前端代码，使用媒体查询(Media Query)做样式适配；在手机端采用另一套代码，例如常见的：[https://m.taobao.com](https://m.taobao.com) 以及 [https://m.baidu.com](https://m.baidu.com)，于此同时，多使用Flex布局、Grid布局以实现不同手机设备的兼容。
4. 采用动态设置meta viewport的方式（待更新）。

**[⬆ 回到顶部](#目录结构)**

## ES2017中async和await关键字有什么作用？
ES2017中的async/await关键字是为了更加便捷的实现异步编程而产生的新语法，其本质是包裹在Promise之上的语法糖。

用法: 当使用async关键字修饰某个函数后，该函数的返回值就变成一个包裹了原函数返回值的Promise对象，而不再是简单的返回一个值了。而await关键字只能放在async函数内部才能生效，await应该被放置在任何基于Promise的异步方法之前( Eg: `Promise.resolve('ES2017')` )，此时，当代码逻辑执行到await那一行时，会暂停当前代码执行，直到Promise的状态变成已完成( `fulfilled` )后，才会去返回结果。

优点：
1. 写出的代码更加的简洁、易于维护。
2. 写出的代码易于代码调试，因为使用async/await关键字后，代码执行的变成了同步的，而Promise无法加断点进行调试。

缺点：
1. 让代码的执行变得同步化，await之后的代码，会等待await行执行完成后才去执行。
2. 代码写起来变得繁琐，必须把await行的promise写到async函数里才能生效。

**[⬆ 回到顶部](#目录结构)**

## 请举例说说网站优化的方法有哪些？
对于前端工程师来说，网站优化主要可以从以下这几个方面着手：减少页面http请求数，让服务器发回的资源体积尽量变小，使用缓存，减少DNS域名解析时间，做网页SEO、HTML结构语义化

1. 减少页面http请求数
- 合并页面中的公共资源到一起：CSS、JS、图片(CSS Sprite)
- 使用字体图标iconfont或者内联SVG图片(当svg图片体积较小时)的方式
- 甚至可以将JS和CSS资源压缩后直接输出到页面。Eg: 百度、Youtube等

2. 让服务器发回的资源体积尽量变小
- 压缩JS、CSS、HTML、图片资源后，再从服务器端发送给浏览器。Eg：使用webpack、YUI、gzip等打包工具

3. 使用缓存
- 使用script、link等外部标签引用JS、CSS资源，浏览器会去缓存
- 使用CDN缓存

4. 减少cookie的带宽消耗
- 编码时尽量控制cookie大小体积，消除不必要的cookie
- 当请求静态资源时，不去发送页面cookie，减少带宽消耗。具体做法将静态资源，如图片等，放在子域名下或者另一个域名下

5. 减少DNS域名解析时间
- 当网站请求其他网站资源，发出跨域请求时，可以使用dns-prefetch属性。该属性会去让浏览器提前解析跨域DNS，减少由于域名解析带来时间延迟
```
<link rel="dns-prefetch" href="https://fonts.gstatic.com/">
```

6. 做网页SEO、HTML结构语义化
- 给网站添加description、keyword等meta标签，让搜索引擎更易爬取到页面内容
- 前端工程师在写html结构时，应该注意代码结构的语义化，在适当的位置使用`h1-2标签`、`a标签`、`图片alt属性`等

**[⬆ 回到顶部](#目录结构)**

## 请说说你对前端模块化编程的理解?
前端模块化编程的出现，主要是为了解决前端领域两个一直存在的问题。  
1. 块级作用域的问题
2. 不同js文件之间相互依赖的问题

除此之外，模块化编程还使得前端开发变得更加工程化，易于代码的开发和维护。  

常见的模块化标准有CommonJS、AMD、ES Module。  
其中，CommonJS为Node.js的一套模块化规范，运行在Node环境下，使用require函数和module.exports对象来实现模块的导入导出。例如：  
```
const moduleA = require('./moduleA'); // 导入（引用）moduleA
module.exports = moduleA;             // 导出（定义）moduleA
```
AMD是一套运行在浏览器端的模块化规范，不同于CommonJS的同步加载，AMD默认采用异步模块加载的方式。分别使用require和define函数来实现引用和定义。此处使用[require.js](https://requirejs.org/)进行举例：
```
// 定义模块A
define('moduleA', ['moduleB'], function(moduleB) {
  // 1. 第一个参数moduleA为模块A的名称
  // 2. 第二个参数moduleB为moduleA所依赖的其他模块
  // 3. 第三个参数中的moduleB为模块B所导出的内容

  return 'moduleA ' + moduleB;
})；
```
```
// 引用模块A
require(['moduleA'], function(moduleA) {
  console.log(moduleA); // 输出'moduleA moduleB'
});

```
ES Module是在ES6中引入的模块化规范，目前使用也最为广泛，使用import和export两个关键字进行导入导出，例如：
```
// moduleA.js
const moduleA = new Date().getTime(); // 定义模块A
export default moduleA;               // 导出模块A
```
```
// index.js
import moduleA from './moduleA';      // 导入模块A
console.log(moduleA);                 // 使用模块A
```
特别值得一提的是UMD并不是一套模块化规范，它只是抹平不同模块差异的一种编码模式，使得编写的模块在不同环境都能够正常运行。具体请参考[代码示例](https://github.com/tjcchen/interviews/blob/master/UMD/random.js)。

**[⬆ 回到顶部](#目录结构)**

## Git常规操作当中的reset, rebase, revert, merge, fetch在哪些时候会被用到以及它们的不同之处?
git reset/rebase/revert/merge/fetch 的区别是什么

**[⬆ 回到顶部](#目录结构)**

## 请说说你对虚拟DOM的理解？
虚拟DOM的实质是用JavaScript对象去描述真实DOM的节点。它的出现使得页面渲染的性能有了很大程度的提升，主要归功于diff函数在做更新操作时，通过新旧虚拟DOM树的比对，只去更新那些需要更新的DOM节点或者属性，并将结果渲染在真实DOM上。虚拟DOM其实并不神秘，在使用虚拟DOM描述一个Div元素时，其结构大致为：
```
<div id="app">virtual dom</div>

转换为：

const vdom = {
  tagName: 'div',
  attrs: {
    id: 'app'
  },
  children: [
    'virtual dom'
  ]
};
```
以ReactJS为例来说明，构建虚拟DOM的几个重要函数：`createElement`、`render`、`mount`、`diff`.  
createElement(): 通过该方法来创建虚拟DOM树。  
render(): 通过该方法来将虚拟DOM树转换为真实DOM节点。  
mount(): 将真实DOM节点挂载到root节点下。  
diff(): 当有更新操作时（属性更新或者节点更新），进行新旧两棵虚拟DOM树的比对，只去更新那些需要更新的部分。

具体代码实现部分，可参考[代码示例](https://github.com/tjcchen/simple-virtual-dom/)

**[⬆ 回到顶部](#目录结构)**

## 节流(throttle), 防抖(debounce), 函数柯里化(currying)在实际工程中有什么作用并且简述下其原理?
节流和防抖的作用类似，主要用于限制高频事件的触发。而函数柯里化使得函数(`function`)的调用变得更加灵活，我们可以一次性传入几个或者多个参数调用函数。类似的例子有：connect(mapStateToProps)(Component) 或者 add(1)(2)(3)；

节流的实现原理：使用时间戳来控制，在一段时间内，某个事件只能触发一次。具体代码实现为：
```
const throttle = (fn, delay = 250) => {
  let last = 0;

  return (...args) => {
    const that = this;
    const now = new Date().getTime();

    if (last + delay > now) {
      return;
    }

    last = now;
    return fn.apply(that, args);
  };
};
```
防抖的实现原理：使用timer来控制一段时间内，某个事件只触发一次。具体代码实现为：
```
const debounce = (fn, delay = 250) => {
  let timerId = null;

  return (...args) => {
    if (timerId) {
      clearTimeout(timerId);
      timerId = null;
    }

    const that = this;

    timerId = setTimeout(() => {
      fn.apply(that, args);
    }, delay);
  };
};
```
函数柯里化的实现原理：使用`闭包`或者`bind函数`实现函数参数的分开多次传入。这里我们使用闭包来做一个简单的实现：
```
const add = (...args) => {
  let sum = 0;

  function helper(...arguments) {
    args = args.concat(arguments);

    sum = args.reduce((accum, curr) => {
      return accum + curr;
    });

    return helper;
  };

  helper.toString = function() {
    return sum;
  };

  return helper;
};

const sum = +add(1)(2, 3)(4, 5, 6)(7)(8)(9, 10); // '+'操作符会把字符串转为数字 
console.log(sum); // 55
```

节流和防抖的区别在于：节流会每隔一段时间去触发一次高频事件，当用户第一次触发事件时，会去执行一次事件函数调用，以后每隔一段时间都会去触发该事件。而防抖会在用户停止高频事件触发后，间隔一个延迟时间，才去执行一次事件函数调用。

节流应用场景：用户滚轮事件onscroll、用户频繁的提交购物车事件  
防抖应用场景：窗体拖动事件onresize、用户搜索框触发的输入匹配事件  
柯里化应用场景：`add(1)(2, 3)(4)(5)`函数、Redux中的`connect`函数将属性和组件联系起来

**[⬆ 回到顶部](#目录结构)**

## 说说你对跨域问题的理解？
常见实现跨域的技术有JSONP、CORS、PostMessage、IFrame、代理等

**[⬆ 回到顶部](#目录结构)**

## 常见的网站攻击有哪些，如何通过编码做到相应的防护？
网站的常见攻击有XSS、CSRF、SQL注入。  
XSS是跨站的脚本攻击(Cross Site Scripting)，是指攻击者将恶意脚本代码注入到网站的一种攻击方式，通过该方式攻击者可以破坏其他用户的网站正常使用，以及窃取用户的敏感信息等。常见的攻击如下：
1. 攻击者在网站的输入框、或者提交评论等位置输入恶意脚本代码，网站直接将用户输入的内容未经处理存储到了数据库,之后又将这些评论直接输出给其他用户看，这样其他用户在访问的网站页面时就会执行恶意代码，造成危险。
修复方式：任何用户输入的内容都去进行escape或者encode处理，才能进行后续的操作，例如
```
<script>window.location.href='http://hackers-website.com';</script>

转译为：

&lt;script&gt;window.location.href=&apos;http://hackers-website.com&apos;;&lt;/script&gt;
```
2. 攻击者给受害者发送钓鱼邮件，邮件中的url里含有恶意脚本，受害者点击链接后，被跳转到某网站，网站直接将url所带的参数输出到页面上。此时用户的敏感信息就会有被盗取的风险。例如：
```
钓鱼网站中包含的链接为：

http://example.com?query=<img src onerror="alert(document.cookie);" />

网站中的部分代码为：

let query = new URL(window.location).searchParams.get('query')
let queryElmt = document.getElementById('query');
query.innerHTML = query; 

// 此时query元素的内容为：query.innerHTML = <img src onerror="alert(document.cookie)" />;
// 用户的敏感信息就有被盗取的风险
```
修复方式：任何赋值给元素innerHTML的内容都要谨慎处理，只去把可信的html内容赋值给它。其他的内容可以先去进行escape转码后，再去赋值。  

3. 其他的一些防止XSS攻击的方法可以配合服务器端一起来做，比如设置内容安全策略响应头部(`Content-Security-Policy`)来限制脚本的来源，或者设置HTST(`HTTP Strict-Transport-Security`)响应头部来限制只能通过https协议访问网站。
服务器端的代码示例：
```
Content-Security-Policy:

response.setHeader("Content-Security-Policy", "script-src http://www.example.com http://www.example2.com");

Strict-Transport-Security:

response.setHeader("Strict-Transport-Security", "max-age=172800")；
```

4. 除此之外，还可以在服务器端给SetCookie设置HttpOnly属性，保证cookie无法通过脚本的document.cookie进行访问，避免敏感信息XSS盗取。HttpCookie通常用在记录服务器端的数据，而浏览器并不需要，如用户登录状态等。代码示例：
```
Set-Cookie: id=a3fWa; Expires=Thu, 21 Oct 2021 07:28:00 GMT; Secure; HttpOnly
```

**[⬆ 回到顶部](#目录结构)**
