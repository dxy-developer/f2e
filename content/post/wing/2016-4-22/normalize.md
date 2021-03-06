+++
title = "Normalize.css学习"
date = "2016-04-25"
tags = ["CSS"]
draft = false
author = "阿wing"
+++

------

Normalize.css 只是一个很小的CSS文件，但它在默认的HTML元素样式上提供了跨浏览器的高度一致性。相比于传统的CSS reset，Normalize.css是一种现代的、为HTML5准备的优质替代方案。

#### 综述

由于不同浏览器渲染Html元素时的各种默认样式不同，导致渲染页面时效果不一致，css Reset正是为了解决这一问题出现的。但是 css Reset 的激进派的，完全去掉浏览器默认的样式。
所有的样式都由自己实现，即使跟浏览器默认样式一致。

<!--more-->
------
而Normalize.css是改良派,依赖于研究浏览器默认元素风格之间的差异，精确定位需要重置的样式。

* 保护有用的浏览器默认样式而不是完全去掉它们
* 为大部分HTML元素提供一般化的样式
* 修复浏览器自身的bug并保证各浏览器的一致性。

相比于传统的reset，Normalize.css是一种现代的、为HTML5准备的优质替代方案,目前像 Bootstrap Amaze UI等框架都在使用。

* [Normalize.css 项目地址](https://github.com/necolas/normalize.css)

#### 源码分析

Css Reset发展至今，进过了几个版本。第一份css Reset应该是 YUI团队提供的,核心还是清除所有浏览器默认样式

```css
:link,:visited { text-decoration:none }
ul,ol { list-style:none }
h1,h2,h3,h4,h5,h6,pre,code { font-size:1em; }
ul,ol,li,h1,h2,h3,h4,h5,h6,pre,form,body,html,p,blockquote,
fieldset,input{ margin:0; padding:0 }
a img,:link img,:visited img { border:none }
address { font-style:normal }
```

之后出现阿里的Kissy框架，自己定制了一份css Reset，这应该是国内第一份CSS Reset。我们使用的reset.css大部分都是拷贝这个版本。但是所有版本的 CSS Reset 作者 都叮嘱使用者
> 请根据具体需求，适量裁剪和修改后再使用。

Normalize.css并没有完全去除默认样式，否则跟全部用div跟li有什么区别呢。改良的Normalize.css具体改了哪些地方，下面举几个例子
```css
/**
 * Correct `block` display not defined for any HTML5 element in IE 8/9.
 * Correct `block` display not defined for `details` or `summary` in IE 10/11
 * and Firefox.
 * Correct `block` display not defined for `main` in IE 11.
 */

/**
 * Add the correct display in IE 9-.
 * 1. Add the correct display in Edge, IE, and Firefox.
 * 2. Add the correct display in IE.
 */

article,
aside,
details, /* 1 */
figcaption,
figure,
footer,
header,
main, /* 2 */
menu,
nav,
section,
summary { /* 1 */
  display: block;
}
```
* 主要为低版本的IE们补充一些HTML5元素的正确显示方法。

在遇到不识别的标签时，浏览器会解析称内联元素，
但是测试了下并不能解决实际性的问题，IE8下还是不识别；主要可以统一各元素的显示方式。

```css
/**
 * Prevent `sub` and `sup` elements from affecting the line height in
 * all browsers.
 */

sub,
sup {
  font-size: 75%;
  line-height: 0;
  position: relative;
  vertical-align: baseline;
}

sub {
  bottom: -0.25em;
}

sup {
  top: -0.5em;
}
```
* 防止所有浏览器中的sub和sup影响行高，就把两者的line-height设为0，然后用top和bottom手动设置两者偏移量。


#### 如何使用

1. npm install normalize.css
2. 引入 normalize.css 源码并在此基础上构建，在必要的时候用你自己写的CSS覆盖默认值

Normalize.css 被拆分为多个独立的部分，这样你就可以定制自己所需要的，可以选择性地移除掉不会用到部分。
比如在移动端使用的时候，就可以把为了兼容IE的部分移除。


#### 参考资料
1. [https://segmentfault.com/a/1190000003025718](https://segmentfault.com/a/1190000003025718)
2. [http://jerryzou.com/posts/aboutNormalizeCss/](http://jerryzou.com/posts/aboutNormalizeCss/)