# 前端面试常见问题以及答案（简洁版）

## 项目介绍
该项目用来覆盖常见的前端面试问题，使用中文和Markdown来完成项目的制作。市面上已经有很多类似的项目了，但是问题和答案都非常的冗长，该项目力求使用简洁的文字来回答面试官所问到的常见问题，希望对您的前端面试有所帮助。

## 目录结构
- [请说说你对闭包的理解?](#说说你对闭包的理解)
- [请解释下浮动问题以及相应的解决方案?](#请解释下浮动问题以及相应的解决方案)
- [如何实现使用CSS实现文字截断效果?](#如何实现使用CSS实现文字截断效果)
- [请说说你对BFC的理解以及相应的应用场景？](#请说说你对BFC的理解以及相应的应用场景)
- [请说说你对响应式布局的理解以及如何实现？](#请说说你对响应式布局的理解以及如何实现)

## 说说你对闭包的理解?
闭包

**[⬆ 回到顶部](#目录结构)**

## 请解释下浮动问题以及相应的解决方案？
清除浮动

**[⬆ 回到顶部](#目录结构)**

## 请说说你对BFC的理解以及相应的应用场景？
BFC

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
3. 使用相对/绝对定位（positive:relative/absolute;）配合伪类元素(:after)进行实现

**[⬆ 回到顶部](#目录结构)**

## 请说说你对响应式布局的理解以及如何实现？
响应式布局

**[⬆ 回到顶部](#目录结构)**

## 协议
[MIT](https://github.com/tjcchen/questions-and-answers/blob/main/LICENSE)