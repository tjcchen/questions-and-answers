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
- [请简述下Session Token和JWT的区别和应用场景？](#请简述下Session-Token和JWT的区别和应用场景)
- [说说你对Flex布局和Grid布局的理解？](#说说你对Flex布局和Grid布局的理解)

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
3. PC端和平板电脑端采用一套前端代码，使用媒体查询(Media Query)做样式适配；在手机端采用另一套代码，例如常见的：[https://m.taobao.com](https://m.taobao.com) 以及 [https://m.baidu.com](https://m.baidu.com)，同时，多使用Flex布局、Grid布局以实现不同手机设备的兼容。
4. 采用动态设置meta viewport的方式（待更新）。

**[⬆ 回到顶部](#目录结构)**

## ES2017中async和await关键字有什么作用？
ES2017中的async/await关键字是为了更加便捷的实现异步编程而产生的新语法，其本质是包裹在Promise之上的语法糖。

用法: 当使用async关键字修饰某个函数后，该函数的返回值就变成一个包裹了原函数返回值的Promise对象，而不再是简单的返回一个值了。而await关键字只能放在async函数内部才能生效，await应该被放置在任何基于Promise的异步方法之前( Eg: `Promise.resolve('ES2017')` )，此时，当代码逻辑执行到await那一行时，会暂停当前代码执行，直到Promise的状态变成已完成( `fulfilled` )后，才会去返回结果。

优点：
1. 写出的代码更加的简洁、易于维护。
2. 写出的代码易于添加断点调试，因为使用async/await关键字后，代码执行的变成了同步的，而Promise无法加断点进行调试。

缺点：
1. 让代码的执行变得同步化，await之后的代码，会等待await行执行完成后才去执行。
2. 代码写起来变得繁琐，必须把await行的promise写到async函数里才能生效。

**[⬆ 回到顶部](#目录结构)**

## 请举例说说网站优化的方法有哪些？
对于前端工程师来说，网站优化主要可以从以下这几个方面着手：减少页面http请求数，让服务器发回的资源体积尽量变小，使用缓存，减少DNS域名解析时间，做网页SEO、HTML结构语义化

1. 减少页面http请求数
- 合并页面中的公共资源到一起：CSS、JavaScript、图片(CSS Sprite)
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
在回答该问题之前，先在这里简述下，将一个本地仓库添加到github远端仓库的过程：
- 本地有一个文件夹，我们把它变成一个拥有git版本记录功能仓库：`git init`
- 在本地添加完文件，进行了本地commit操作后，把该仓库推送到github远端：`git remote add origin git@github.com:tjcchen/test.git`  
注意：这里的origin是远端地址的别名，远端地址指的是 `git@github.com:tjcchen/test.git`
- 将本地代码推送到远端：`git push -u origin main`  
注意：这里的 `-u` 是 `--set-upstream`，会把远端的main分支设置为默认上游分支，下次直接输入 `git push` 就可以推送到远端main分支
- 此时可以使用 `git remote -v` 查看 push 和 fetch 的远端地址，例如：
```
origin	git@github.com:tjcchen/test.git (fetch)
origin	git@github.com:tjcchen/test.git (push)
```


`git reset`  
git reset命令会去将本地提交退回到之前的某一个版本，但是在指定版本提交之后的代码修改依旧存在。eg:
```
git reset 55646eca9bcb6f5413039b020b1f287b507ea2eb
```

如果想要退回到之前某一个版本，不仅log信息会退回到之前版本，相应的代码也会回到之前的状态，需要使用 `--hard` 这个flag。eg：
```
git reset --hard 55646eca9bcb6f5413039b020b1f287b507ea2eb
```


`git revert`  
git revert命令同样也用于将本地代码退回到之前的某一个版本，但是和git reset的区别在于，会在git log信息当中，多增加一条commit信息，用于说明revert操作。eg:
```
git revert 55646eca9bcb6f5413039b020b1f287b507ea2eb

代码退回到之前版本的同时，增加如下log信息，该log信息也包含hash头，是一次新的commit提交

commit 6b57017c3ea6d9e4806b1b6e4ad72386559597ab

Revert "add a new feature"
This reverts commit 55646eca9bcb6f5413039b020b1f287b507ea2eb.
```


`git rebase`  
git rebase命令，该命令中的rebase，被翻译为“变基”，意味着会去改变之前提交的基准。通常会在两种情况下被使用到：1. 自己在本地进行代码提交时，对之前的提交log信息做一定的修改( 此时，代码并没有提交代码到远端仓库 )。2. 去和别的分支进行合并代码的时候  

1. 自己在本地进行代码提交时，对之前的提交log信息做一定的修改  

在第一种情况下，需要使用 `git rebase -i` 命令，这里 -i 代表 interrupt, 例如:
```
git rebase -i 55646eca9bcb6f5413039b020b1f287b507ea2eb

此时，命令行会进入一个交互式的git操作页面，在选择对应操作后，编辑文件，退出即可完成操作，必要时还需要做一定的代码修改。常见的操作有:  

reword 更改某一次提交的log信息
squash 将之前两次连续提交的log信息进行合并
drop 放弃某次提交
edit 将某些新的代码修改加到之前的某次提交当中去

以及修改某两次提交的前后顺序等
```

2. 去和别的分支进行合并代码的时候  

除了上面的操作之外，git rebase命令还能用来有效的合并分支，合并完成的分支，会产生干净的log信息提交链条，没有多余的merge提交信息。例如在一个feature分支上开发新功能，但是master分支在分叉以后，又有别的代码提交了进去，此时想把master分支的提交也同步到feature分支，可以使用：`git rebase master` 命令，此时，feature分支会将master分支在分叉之后的代码合并到feature分支上，并产生干净的log信息链条。

同时，将一个功能分支(feature)合并到主分支(master)，也十分的方便，并且会产生干净的log信息链条。例如：`git rebase feature`。

另外，当有其他的开发者已经将代码提交到远端，并且他的修改和自己的修改有冲突时，可以做如下操作：
- fetch远端master分支代码到本地的remotes/origin/master分支：`git fetch origin master`  
注意：此时当切换到本地的remotes/origin/master分支，查看最新的远端代码，可以使用命令 `git checkout remotes/origin/master` 或者 `git checkout origin master`
- 使用远端master分支的本地备份分支，即remotes/origin/master，作为基准，在其之上再做代码修改：`git rebase origin/master`
- 此时，当修改完成后在进行代码的提交和push，会产生干净的log信息链条


`git merge`  
git merge命令用于不同分支的合并，一般用法如下，将feature分支合并到master分支：
```
在master分支下执行：

git merge feature
```
该种merge方式，会把feature的所有提交信息一并也都显示到master分支的log信息下，并且会产生一条新的merge commit信息。

如果不想在master分支也同时显示feature分支的log信息，可以使用如下命令：
```
git merge --squash feature
```
但是，需要自己手动在master分支再去提交一次合并feature分支的信息，好处是log信息链条更加可控。

以上两种merge方式的选择，需要结合自己的业务开发场景。


`git fetch`  
git fetch命令用于将远端的分支更新到本地的远端分支备份，多用于团队合作之前，合并别人有冲突的代码。例如：
```
git fetch origin master
```
该命令会将远端的master分支fetch到本地的remotes/origin/master分支，此时remotes/origin/master分支上为远端最新的代码


`git pull`  
git pull命令，会将远端的代码拉倒本地，并且去做一个merge操作。其实质是一共执行了两个命令操作：git fetch和git merge。举例简单来描述下该过程：  
```
git pull origin master
```
- 该命令先会去将远端master分支上的代码更新到本地的remotes/origin/master分支上，实际执行了 `git fetch origin master`
- 紧接着将本地备份分支的代码，即本地origin/master分支，和master主分支进行了合并。相当于在master分支执行 `git merge origin/master`

注：可以使用该命令查看所有的本地分支：`git branch -al`

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

response.setHeader("Strict-Transport-Security", "max-age=172800");
```

4. 除此之外，还可以在服务器端给SetCookie设置HttpOnly属性，保证cookie无法通过脚本的document.cookie进行访问，避免敏感信息XSS盗取。代码示例：
```
Set-Cookie: id=a3fWa; Expires=Thu, 21 Oct 2021 07:28:00 GMT; Secure; HttpOnly
```

CSRF攻击是跨站请求伪造攻击(Cross Site Request Forgery)，攻击者通过获取真实用户的登录认证信息(authentication)，来向服务发起伪造请求，
从而达到攻击网站用户的效果。常见攻击为修改用户密码、删除用户账号、和进行银行转账等。

举一个简单的例子来说明原理：
- 当用户通过用户名和密码登录某银行网站(eg: `http://www.bank.com`)后，银行向用户发送了一个session_token用来记录用户的登录状态（使用cookie来存储）
- 这时，该用户收到了一封钓鱼邮件，诱导用户跳转到某非法网站，网站的部分代码大致如下：
```
<body onload="document.csrfForm.submit()">
  <h3>Forgery Form Used for CSRF DEMO</h3>
  <form action="http://www.bank.com/transfer" method="POST" target="hiddenFrame" name="csrfForm">
    <input type="hidden" name="name" value="bob" />
    <input type="hidden" name="amount" value="100000" />
  </form>
  <iframe name="hiddenFrame" style="display:none;"></iframe>
</body>
```
- 上面所示的这段代码会在页面加载完成后，向银行发送一个post请求，用来伪造用户的操作。大致请求为：
```
url: http://www.bank.com/transfer
method: POST
name: bob
amount: 100000
session_token: ejicnieu448unfnd32993jenfncx
```
- 此时由于钓鱼页面发来的请求和用户自己操作时的请求一样，同样都带有session_token，而且其他参数也都一致，所以银行认为是用户的操作，完成了转账操作。
- 至此，一个简单的CSRF攻击就得以实现

修复方式：
- 使用CSRF Token的方式，从服务器向浏览器发送token，下次用户再访问网站其他页面时，会将CSRF Token和Session Token一个发回网站进行认证。(推荐)
- 在用户关键操作时，如转账、修改密码时，再次认证用户登录信息，通过输入用户名密码、填写验证码、或者发送短信等方式。


SQL注入是一种常见的数据库攻击，在代码层面，后端工程师需要使用参数化SQL的方式，避免该攻击。例如在Java当中使用PreparedStatement

**[⬆ 回到顶部](#目录结构)**

## 请简述下Session Token和JWT的区别和应用场景？
首先Session Token和JWT(Json Web Token)都是用于维持用户登录状态的技术。

Session Token技术将用户的登录状态信息保存在cookie当中，从服务器端通过Set-Cookie响应头部发送给浏览器，下次用户在访问网站的其他页面时，还会将相应的Session Token包含在cookie当中，一起发回给服务器进行认证，从而实现用户身份信息的认证。该种技术多应用于传统的BS架构（Browser and Server）的网站。

JWT(Json Web Token)技术的实现强烈依靠加密算法，需要将用户的用户名等信息放在一起，进行加密后，以密文的形式发送给客户端。当用户再次进行访问服务器其他功能时(通常以REST API的方式)，
还需将JWT的token一起通过http请求头部带给服务器端进行认证。该种技术多用于前后端分离的网站应用，以及Android和IOS手机应用当中。

需要注意的是：Session Token当中包含的信息只是用户登录的凭证，可以是用户的ID等，通常会临时保存在服务器端的缓存(Redis/Memcached)或者数据库(Postgre/MongoDB)当中，就算不小心token被盗用了，也不会产生影响，因为该凭证只和自己的服务器有对应关系。
而JWT发回给用户的token是包含了用户名、邮箱等信息的密文，会被保存在客户端，因此密文的安全性变得十分重要。

经过加密的JWT token，通常包含三个部分：头部(header)，消息体(payload)，签名(signature)。使用点分隔符（.）进行分割。例如：  
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.  
eyJkYXRhIjp7ImlkIjoxMDAwMDEsInVzZXJuYW1lIjoid2VicGFjayIsImVtYWlsIjoidGVzdEBxcS5jb20iLCJhdmF0YXIiOiIvL3FwaWMudXJsLmNuL2ZlZWRzX3BpYy9hak5WZHFIWkxMQks3UXlKbmljTXVpY3dXVnJLaHVJYzQyNndFWWJJYVNsYVhaUkR1cXMyaDRYQS8iLCJ0eXBlIjoyfSwiZXhwIjoxNTY5NjYyNDkyLCJpYXQiOjE1NjkwNTc2OTJ9.  
_cc7B2Q565rL-hKK25Lppw4IDVEkQP17qky0boVTlrA

一个简单的通过curl模拟发送jwt到服务器端的例子如下：
```
curl -H 'authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJkYXRhIjp7ImlkIjoxMDAwMDEsInVzZXJuYW1lIjoid2VicGFjayIsImVtYWlsIjoidGVzdEBxcS5jb20iLCJhdmF0YXIiOiIvL3FwaWMudXJsLmNuL2ZlZWRzX3BpYy9hak5WZHFIWkxMQks3UXlKbmljTXVpY3dXVnJLaHVJYzQyNndFWWJJYVNsYVhaUkR1cXMyaDRYQS8iLCJ0eXBlIjoyfSwiZXhwIjoxNTY5NjYyNDkyLCJpYXQiOjE1NjkwNTc2OTJ9._cc7B2Q565rL-hKK25Lppw4IDVEkQP17qky0boVTlrA'
-X POST -d "title=test&content=test&thumbnail=http://www.tjcchen.cn/love.png" "http://127.0.0.1:8001/v1/review/new"
```
**[⬆ 回到顶部](#目录结构)**

## 说说你对Flex布局和Grid布局的理解?
Flex布局和Grid布局都是为了更好的实现响应式布局而产生的CSS新语法。这两种布局多用于响应式网站页面和手机端页面。

Flex布局  
实现Flex布局，一共有两部分的内容需要注意：
1. 第一步是要在父容器设置 `display:flex;` 属性，告诉浏览器，父元素中包裹的子元素要使用flex方式进行布局了
2. 第二步是要在子元素当中设置 `flex:1;` 属性，用于告诉浏览器，该子元素要以多少比例进行缩放，子元素会根据浏览器宽度的一定比例动态设置子元素宽度
```
<div class="container">
  <div class="item1"></div>
  <div class="item2"></div>
  <div class="item3"></div>
</div>

CSS:

.container {
  display: flex;
  flex-direction: row; /* 默认方向为row，会横向展示item的内容; 另一个direction为column */

  /* 下面内容做属性值参考，先给注释掉 */
  /* flex-wrap: wrap; 浏览器宽度缩小会换行 */
  /* align-items: stretch; 默认值，会纵向撑慢容器；其他值还有 flex-start, flex-end, center */
}

.container .item1 {
  flex: 1; /* 等同于 `flex:1 1 0;` flex是一个合并属性，对应属性为 `flex:flex-grow flex-shrink flex-basis;` */
}
.container .item2 {
  flex: 2; /* 会以 `flex:1;` 两倍的宽度进行缩放，`flex:1` 代表子元素会按照窗体宽度的一定比例进行缩放，会填满父容器可用空间 */
}
.container .item3 {
  flex: 1 0 30%; /* 此时 `flex-basis` 为30%，为item3的默认宽度， `flex-shrink` 为0，代表不去收缩 */
}
```

Grid布局也可以很容易的实现响应式布局，Grid的基本理念为将页面元素划分为一个一个的网格，然后指明每个子元素需要占取的网格数量。实现Grid布局也有两个部分需要注意，即父元素和子元素部分，但大部分设置都集中在父元素。
1. 第一步要在父元素中设置 `display: grid;` 属性，除此之外，还要在父元素中指明子元素的网格列数和行数，通过宽度和高度设置，例如：
```
.container {
  display: grid;
  grid-template-columns: 300px 200px 300px; /* 指明一共有三列，第一列300px，第二列200px，第三列300px */
  grid-template-rows: 200px 100px;          /* 指明一共有两行，第一行200px，第二行100px */

  /* 下面内容做属性值参考，先给注释掉 */
  /* 如果有多列，每列宽度一行，也可使用repeat来做重复，下例中的4代码重复4次，即4列 */
  /* grid-template-columns: repeat(4, 300px); */

  /* 该属性设置有三列，左列宽度固定，为220px，中间列宽度1个fraction，右列宽度为auto为自动填充 */
  /* 其中 1fr 为一个新单位，为1个fraction，会去占用父元素的剩下可用空间；2fr代表会占用1fr的两倍空间 */
  /* grid-template-columns: 220px 1fr auto; */

  /* [有用]：auto-fit属性会去自动伸缩子元素宽度去填满容器 */
  /* 而 auto-fill 会去使用空元素占位置填满剩余的空间 */
  /* grid-template-columns: repeat(auto-fit, minmax(60px, 1fr)); */

  /* 该属性会去自动使用子元素填满父容器，当元素跨行/列的子元素所占宽高不合理时 */
  /* grid-auto-flow: dense; */

  /* 该属性设置默认行的高度，最小高度为150px */
  /* grid-auto-rows: minmax(150px, auto); */

  /* 设置网格间距，使用gap */
  /* 等于gap-row: 10px; gap-column: 20px; */
  /* gap: 10px 20px; */
}
```
2. 第二步要在子元素中，设置每个元素所占的网格数，例如：
```
.container .item1 {
  grid-column: 1 / 4; /* 等同于：grid-column-start: 1; grid-column-end: 4;, 表示item1占取三列 */
  grid-row: 1 / 3;    /* 等同于：grid-row-start: 1; grid-row-end: 3;, 表示item1占取两行 */
}

或者

.container .item2 {
  grid-column: span 3; /* item2占取三列 */
  grid-row: span 2;    /* item2占取两行 */
}
```

除此之外，可以使用 `grid-content:end; justify-content:center;` 类似属性，设置父元素的位置，`align-items:center; justify-items:center;` 
去设置子元素在父元素网格中的位置，以及 `align-self:start; justify-self:end;` 去覆盖父元素设置的位置。

Flex布局和Grid布局的不同之处在于, Flex设置的是单一维度的响应式布局(横轴或者纵轴)，而Grid布局设置的是两个维度的，即横纵维度的布局。

**[⬆ 回到顶部](#目录结构)**