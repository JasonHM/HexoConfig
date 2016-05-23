title: angular js
date: 2016-03-06
tags: 
    - angularjs
categories: 编程

---

angularjs

route: 

ngRoute -> ng-view

ui-route -> ui-view

在单页面应用局部刷新好用,route的功能能够精确定义到在哪个功能区,加快了页面的反应速度。在web端响应即及时,在手机端有比较明显的'闪屏'(闪一下屏幕)。

ng-inClude能过分割页面，较大的页面可以被分为多个页面逐个应用。

ng不能与js里面的`script`及时的交互,每次执行`js`语句的时候需要延时运行，等页面加载出来。

例如: 

```
<p class='title'>{{title}}<p>
<script>
$(".title").text(); //这种情况会在页面没有加载的时候就执行,拿到的结果为空。
setTimeout(function() {
	$(".title").text();
}
</script>

```
