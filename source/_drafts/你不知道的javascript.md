title: 你不知道的JavaScript 阅读笔记
date: 2015-10-26 11:21:56
tags:

---


LHS查询： 查找的目的是对变量进行复制
RHS查询： 获目的是获取变量的值

严格模式下禁止自动或隐式的创建全局变量,如下:

```
"use strict";
function foo(a){
    console.info(a + b);  //ReferenceError: b is not defined
    b = a;
}
foo(2);
```
严格模式下 `eval()`和`with`会受到影响（限制）。 `eval()`有自己的语法作用域
