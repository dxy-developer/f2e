+++
categories = ["Promise"]
date = "2016-04-18"
description = ""
tags = ["Promise"]
title = "初探 Promise"
author = "acrens"
+++

曾经有伟人说过，对于一件新鲜事物，如果需要搞明白他，就会有以下三个步骤：What、How、Why（学习、思维三部曲 或 叫做学习黄金圈）；而对于很多人，在学习一门技术时，都停留在 What 阶段，到使用时就不知道如何使用，就算使用了也不知道为什么要用。<!--more-->
![黄金圈](../whw.png)

---

### What（Promise 是什么）

#### 描述
Promise 是抽象异步处理对象以及对其进行各种操作的组件，而且 Promise 并不是从 JavaScript 中发祥的概念。
#### 状态
Promise 具有三种状态，分别为 pending（执行中）、resolved（被接受）、rejected（被拒绝）。
#### 方法
实例化：

* var promise = new Promise(function(resolve, reject) {});
* Promise.resolve() 等方法均可以直接返回一个新创建的 Promise 对象。

静态方法：Promise.all、Promise.race、Promise.resolve、Promise.reject：

* Promise.all()

> Promise.all 方法为 Promise 组件的静态方法，无需创建 Promise 对象就可以直接使用此方法来并行执行多个 Promise 对象，且在 Promise.all(["Promise1"，"Promise2"， "Promise2"])，如果在 all 方法参数的数组中有一个 Promise 对象执行失败即停止执行，返回结果需要等到数组对象执行完成才返回最后结果，结果为多个 Promise 对象返回值组成的数组。
> 
> 代码：
> var p1 = Promise.resolve(1)；
> var p2 = Promise.resolve(2)；
> var p3 = Promise.resolve(3);
> Promise.all([p1, p2, p3]).then(function(results) {
> console.log(results);  // [1, 2, 3]
> });

* Promise.race()

> Promise.race 方法性质同 Promise.all 方法，使用方式也一样，但是有一点不同是在 Promise.race(["Promise1"，"Promise2"，"Promise3"]) 等到数组参数里面第一个 Promise 对象执行完成就返回执行结果（这里说的第一个不是第一个参数，也可能是第二个，是指第一个执行完成的 Promise 对象）。
> 代码：Promise.race([new Promise(), new Promise(), new Promise()])；

* Promise.resolve()

> 这是一种直接到达 Promise resolved 状态的快捷方式，并且创建返回一个 Promise 对象。
> 代码：
> Promise.resolve("acrens").then(function(name) {
> console.log(name); // acrens
> });

* Promise.reject()

> 同理，这是达到 Promise rejected 状态的快捷方式，并且创建返回一个进行 reject 的新 Promise 对象。如果传入的参数为一个 Promise 对象，则返回的是一个新的 Promise 对象（和 resolve 不同）。
> 代码：Promise.reject(new Error("error"))；

对象方法：new Promise().then、new Promise().catch：

* then()

> 用于注册 Promise 分别达到 resolved、rejected 状态时的回调函数，如：then(resolve, reject)，当达到 resolved 状态时，执行 resolve 方法，否则，执行 reject 方法；reject 函数可以不在此注册，可以使用 catch 注册（这也是注册 reject 方式的语法糖，更方便 Promise 链方法）；如果不需要注册 resolved 状态时的回调函数，then 方法第一个参数不可以省略，但是可以 then(undefined, reject) 这样书写。
> 代码：
> var promise = new Promise(function(resolve, reject) {
> resolve(2);
> });
> 
> promise.then(function(value) {
> console.info('Task --------- ' + value); // Task  --------- 2
> }).catch(function onRejected(error) {
> console.error(error);
> });

* catch()

> catch 方法在此就不多赘述，其只是注册 rejected 状态回调函数的语法糖。
> 代码：（参照上面 then 方法代码示例）。

---

### How（Promise 如何运行）
Promise 从实例化到执行完成可以参照下图并结合上述代码理解（只有认真地去理解这个流程图，才可以看到 Promise 的精髓，坏笑...）：
![执行流程](../flow.png)
注意：fulfill 就相当 resolved 状态。

---

### Why（Promise 为什么会产生）
Promise 需要解决的问题也就是其产生的原因（废话）：

* 异步问题

> 用异步的方式来表达异步的代码是艰难的，甚至很难用我们的大脑来理解。（事件轮询、并发模式）

* 回调地狱

> 并不是简单地理解为代码嵌套，编辑器代码缩进空格；还包括代码的控制转移（如在回调之前进行的第三方调用，控制权转交给第三方）。

--- 
### 总结
在项目开发中，时常会使用到异步处理及代码多层嵌套，这对于后期理解和维护代码是一个“坑”，因此可以尝试使用 Promise 方式去解决代码给后期带来的负担。

*  https://www.web-tinker.com/search/Promise%20%E6%8A%80%E6%9C%AF%E7%BB%86%E8%8A%82/1.html
*  http://liubin.org/promises-book/#introduction
*   http://www.zhangxinxu.com/wordpress/2014/02/es6-javascript-promise-%E6%84%9F%E6%80%A7%E8%AE%A4%E7%9F%A5/
*   http://www.sitepoint.com/overview-javascript-promises/
*  http://blog.getify.com/promises-part-1/ （译文：https://segmentfault.com/a/1190000000586666）
*  https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise

注：下一篇更新 Promise 扩展阅读版
