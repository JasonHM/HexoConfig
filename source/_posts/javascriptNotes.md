title: javascript笔记
tags: 
    - javascript
date: 2015-12-20
categories: 编程

---



# js笔记

## var的作用域

内部函数可以范围外部或全局(不加`var`)的变量,外部不能访问内部函数的变量

<!-- more -->

下面的例子[引用](https://github.com/alsotang/node-lessons/tree/master/lesson11):

```javascript
//第三点: 假设此时外部定义了 childAge
//var childAge = '18';
var parent = function () {
  var name = "parent_name";
  var age = 13;

  var child = function () {
    var name = "child_name";
    var childAge = 0.3;

    // => child_name 13 0.3
    console.log(name, age, childAge);
  };

  child();

  // will throw Error
  // ReferenceError: childAge is not defined
  console.log(name, age, childAge);
};

parent();
```

第一次`console.log`时,会默认先去寻找`child function`中的name对象,找到了则打印,age在本方法中未定义,所以在`child function`的上下文中查找age变量。

第二次console中也是默认寻找`parent`中的`name`变量,此时`childAge`在`parent`中并没有定义,而是在`child function`中定义,js查找`parent function`中没有定义,联系上下文也没有定义,所以此时报错`childAge`没有定义

第三点: 假设我们把第二行代码取消注释，则此时的打印纪录是:

```console
child_name 13 0.3
parent_name 13 18
```
js查找上下文寻找变量的时候不会自己子方法中去查找,在本方中查询不到则回去外部作用域中去查找。

## 闭包

内部函数可以访问定义在外部函数中的变量

```javascript
var adder = function (x) {
  var base = x;
  return function (n) {
    return n + base;
  };
};

var add10 = adder(10);
console.log(add10(5));
// => 15

var add20 = adder(20);
console.log(add20(5));
// => 25
```
上面的例子就是在 第三行 function中 `return n + base`此时在外面拿到返回方法的引用后,再次调用时,此时的`base`则是引用了外部变量（虽然它们都在`adder function`里面） .

下面的代码有时候会经常碰到这个问题，打印的输出为5个`5`,`setTimeout`方法是异步的，当5秒后才回去打印,而此时i的值已经都是5了

```javascript
for (var i = 0; i < 5; i++) {
  setTimeout(function () {
    console.log(i);
  }, 5);
}
```
=>

```javascript
for (var i = 0; i < 5; i++) {
  (function (idx) {
    setTimeout(function () {
      console.log(idx);
    }, 5);
  })(i);
}
```
使用一个`function`包裹之后,这时候每次`console.log`的时候就不会受外层`i`的影响,默认查找`idx`,能够输出 `1,2,3,4,5`了

## js事件的处理顺序

先将主函数处理完成,遇到事件将事件加入到队列中,主函数完成后按队列顺序执行。

## js数组

```javascript
var numbers = ['zero', 'one', 'two', 'three', 'fore'] 
```

数组`numbers`第一个值获得属性名'0',第二个值获得属性名'1',所以能够通过numbers[0]取得zero的值
对象的字面量:

```javascript
var numbers_object = {
    '0':'zero',
    '1':'one',
    '2':'two',
    '3':'three',
    '4':'fore'
} 
```
numbers与nubmers_objext对比,numbers继承的array.prototype,numbers_object继承的object.prototype。所以numbers继承了很多方法。length属性是一个诡异的属性,length没有上界,不一定等于数组属性的个数。

```javascript
var myArray = [];
myArray.length //0
```
数组最后插入一条记录:

```
numbers.length  = 3; //numbers是['zero', 'one', 'two']
numbers[numbers.length] = 'three'; //nubers是['zero', 'one', 'two', 'three']
numbers.push('fore'); //numbers是['zero', 'one', 'two', 'three', 'fore']
```

