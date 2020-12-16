# 前端面试常见问题以及答案（简洁版）

## 项目介绍
该项目用来覆盖常见的前端面试问题，使用中文和Markdown来完成项目的制作。市面上已经有很多类似的项目了，但是问题和答案都非常的冗长，该项目力求使用简洁的文字来回答面试官所问到的常见问题，希望对您的前端面试有所帮助。

## 目录结构
- [请说说你对闭包的理解？](#说说你对闭包的理解)
- [请解释下浮动问题以及相应的解决方案？](#请解释下浮动问题以及相应的解决方案)
- [如何使用CSS实现文字截断效果？](#如何使用CSS实现文字截断效果)
- [请说说你对BFC的理解以及相应的使用场景？](#请说说你对BFC的理解以及相应的使用场景)
- [请说说你对响应式布局的理解以及如何实现？](#请说说你对响应式布局的理解以及如何实现)
- [ES2017中async和await关键字有什么作用？](#ES2017中async和await关键字有什么作用)
- [请举例说说网站优化的方法有哪些？](#请举例说说网站优化的方法有哪些)
- [请说说你对前端模块化编程的理解？](#请说说你对前端模块化编程的理解)
- [Git常规操作当中的reset/rebase/revert/merge/fetch在哪些时候会被用到以及它们的不同之处？](#Git常规操作当中的resetrebaserevertmergefetch在哪些时候会被用到以及它们的不同之处)
- [请说说你对虚拟DOM的理解？](#请说说你对虚拟DOM的理解)
- [节流/防抖/函数柯里化在实际工程中有什么作用并且简述下其原理？](#节流防抖函数柯里化在实际工程中有什么作用并且简述下其原理)
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
1. 使用额外的标签（不推荐）
```
<div style="clear:both;"></div>
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
3. 推荐方式
```
.clearfix:before, .clearfix:after {
  content: "";
  display: table;
}

.clearfix:after {
  clear: both;
}
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
  display: -webkit-box;         /* 使用-webkit-box布局显示（稍微有些奇怪） */
  -webkit-line-clamp: 3;        /* 显示的行数 */
  -webkit-box-orient: vertical; /* 垂直方向显示内容 */
}
```
3. 使用相对/绝对定位（positive:relative/absolute;）配合伪元素(:after)进行实现

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
ES2017中的`async`/`await`是为了更加便捷的实现异步编程而产生的新语法，其本质是包裹在`Promise`之上的语法糖。当使用`async`修饰某个函数后，该函数的返回值变成了一个`Promise`对象，而不再是直接返回一个值了。而`await`关键字只能放在`async`函数内部才能生效，`await`应该被放置在任何基于`Promise`的异步方法（Eg: `Promise.resolve('ES2017')`）之前，此时，`await`关键字会让代码逻辑暂停到被放置的那行代码，直到`Promise`对象已完成（`fulfilled`），才会去返回结果。

**[⬆ 回到顶部](#目录结构)**

## 请举例说说网站优化的方法有哪些？
网站优化方法

**[⬆ 回到顶部](#目录结构)**

## 请说说你对前端模块化编程的理解?
前端模块化编程的出现，主要是为了解决前端领域两个一直存在的问题。  
1. 块级作用域的问题
2. 不同js文件之间相互依赖的问题

除此之外，模块化编程还使得前端开发变得更加工程化，易于代码的开发和维护。  

常见的模块化标准有CommonJS，AMD(Asynchronous Module Definition)，和ES Module。其中，CommonJS为Node.js的一套模块化规范，运行在Node环境下，使用require函数和module.exports对象来实现模块的导入导出。例如：  
```
const moduleA = require('./moduleA'); // 导入（引用）moduleA
module.exports = moduleA;             // 导出（定义）moduleA
```
AMD是一套运行在浏览器端的模块化规范，不同于CommonJS的同步加载，AMD默认采用异步模块加载。分别使用require和define函数来实现引用和定义。此处使用[requirejs](https://requirejs.org/)举例：
```
// 定义模块A - moduleA
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
// moduleA.js - 定义和导出模块A
const moduleA = new Date().getTime(); // 定义模块A
export default moduleA;               // 导出模块A
```
```
// index.js
import moduleA from './moduleA';      // 导入模块A
console.log(moduleA);                 // 使用模块A
```

**[⬆ 回到顶部](#目录结构)**

## Git常规操作当中的reset/rebase/revert/merge/fetch在哪些时候会被用到以及它们的不同之处？?
git reset/rebase/revert/merge/fetch 的区别是什么

**[⬆ 回到顶部](#目录结构)**

## 请说说你对虚拟DOM的理解？
虚拟DOM的理解

**[⬆ 回到顶部](#目录结构)**

## 节流/防抖/函数柯里化在实际工程中有什么作用并且简述下其原理?
节流，防抖和函数柯里化

**[⬆ 回到顶部](#目录结构)**

## 说说你对跨域问题的理解？
常见实现跨域的技术有JSONP、CORS、PostMessage、IFrame、代理等

**[⬆ 回到顶部](#目录结构)**

## 常见的网站攻击有哪些，如何通过编码做到相应的防护？
XSS, CSRF

**[⬆ 回到顶部](#目录结构)**
