title: ECMAScript 6
date: 2016-03-06
tags: 
    - javascript
categories: 编程

---

let命令,不会变量提升,只作用于当前作用域(块级作用域),不允许重复声明变量;

```
console.log(tmp); // ReferenceError   //TDZ(temporal dead zone -> '死区')开始
let tmp = 'tmp';   //TDZ结束
```

```
function func(arg){
	let arg; //报错
}
```

<!-- more -->

const命令,对常量声明后不可改变;与let相同点:作用域,无变量提升,不可重复声明

解构:

```
let[x,,y] = [1,2,3];
x //1
y //3

var {bar,foo} = {foo: "aaa", bar: "bbb"};
foo // "aaa"
bar // "bbb"
```
用途:
交换变量值:

```
[x,y] = [y,x];
```
返回一个数组:

```
function example(){
	return [1,2,3];
}
var [a,b,c] = example();
```
提取JSON数组

数值的扩展

全局方法: parseInt() parseFloat()移植到Number对象上面。

```
//ES5
parseInt("12.34") // 12
parseFloat("123.45#") //123.45

//ES6
Number.parseInt("12.34") //12
Number.parseFloat("123.45#") //123.45
```

`Number.isInteger()` 判断是否为整数

Math对象扩展

`Math.trunc()` 去小数 `Math.sign()`判断正数负数零 这两个应该常用.

更多在[w3c](http://www.w3schools.com/js/js_reserved.asp)查看

数组的扩展

`Array.from()` 将类似数组的对象和可遍历的对象变为真正的数组

```
let ps = document.querySelectorAll('p');
Array.from(ps).forEach(function(p){
	console.log(p);
})
```

可以接受第二个参数,下面的例子将数组中布尔值为false的成员转为0。

```￼Array.from([1, , 2, , 3], (n) => n || 0) // [1, 0, 2, 0, 3]
```

`Array.of()` 将一组值转换为数组

```
Array.of(3, 11, 8) // [3,11,8] 
Array.of(3) // [3] 
Array.of(3).length // 1
```

对象的扩展

```
function f( x, y ) { 
	return { x, y };}// 等同于function f( x, y ) { 
	return { x: x, y: y};}
```

属性表达式 定义方法名,对象时使用

```
// 方法一 obj.foo = true;// 方法二 obj['a'+'bc'] = 123;
```
...
page 52
