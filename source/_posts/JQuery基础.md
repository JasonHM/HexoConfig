title: JQuery基础
date: 2015-10-22 10:52:55
tags: jquery
---

# JQuery基础

## 基础选择器

- id
- element
- .class
- *
- sele1,sele2,seleN
- ance desc 
- parent child
- prev + next 
- prev ~ siblings


`$("parent allChildren")` `parent`下所有的`child`元素
`$("parent>child")` `parent`第一代的`child`元素
`$("prev+next")` `prev`紧挨着且匹配的唯一元素
`$("prev~next")` `prev`之后着且匹配的多个元素
    
## 过滤器选择

- :first,:last
- :eq(index)
- :contains(text)
- :has(selector)
- :hidden
- :visible
- [attribute=value]
- [attribute!=value]
- [attribute*=value]
- :first-child
- :last-child

`$("li:eq(index)")` `index`从零开始
`$("li:contains('jQuery')")` 过滤含有jQuery的元素,英文区分大小写
`$("li:has(label)")`使用包含的元素名称来过滤,注意`selector`需要加上单引号
`$("input:hidden")`获取`input`全部不可见的元素 
`$("li:visible")`获取`li``display`属性全部不为`none`的元素
`$("li[title='蔬菜']")`  `li`元素中`title`属性获取`蔬菜`元素的选择器
`$("li[title*='果']")` `li`元素中所有`title`中含有`果`的选择器
`$("li:first-child")` 所有`li`中的第一个元素

## 表单选择器

- input
- text
- password
- radio
- checkbox
- submit
- image
- button
- checked
- selected

`$("#frmTest :input")`
`$("#frmTest input:submit")`
`$("#frmTest :image")`不能获取`<img>`，只能获取`<input>`的图像域
`$("#frmTest :button")`只能获取普通的type或者`<button>`的按钮，不能获取提交按钮

## 操作DOM元素

attr()方法的作用是设置或者返回元素的属性，其中attr(属性名)格式是获取元素属性名的值，attr(属性名，属性值)格式则是设置元素属性名的值。
html()方法可以获取元素的HTML内容
text()方法只是获取元素中的文本内容
```javascript
var $content = "<b>唉，我又变胖了！</b>";
$("#html").html($content);
$("#text").text($content);
```
addClass()和css()方法可以方便地操作元素中的样式，前者括号中的参数为增加元素的样式名称，后者直接将样式的属性内容写在括号中
```javascript
$("#content").css({"background-color":"red","color":"#fff"});
```
removeAttr(name)和removeClass(class)分别可以实现移除元素的属性和样式的功能，前者方法中参数表示移除属性名，后者方法中参数则表示移除的样式名
```javascript
$("#content").removeClass("white blue");
$("#content").removeAttr("class");
```
append(content)方法的功能是向指定的元素中追加内容，被追加的content参数，可以是字符、HTML元素标记，还可以是一个返回字符串内容的函数
```javascript
function rethtml() {
    var $html = "<div id='test' title='hi'>我是调用函数创建的</div>"
    return $html;
}
$("body").append(rethtml());
```
appendTo()方法也可以向指定的元素内插入内容，它的使用格式是：

```javascript
$(content).appendTo(selector)
```
参数content表示需要插入的内容，参数selector表示被选的元素，即把content内容插入selector元素内，默认是在尾部。

```javascript
<script type="text/javascript">
    var $html = "<span class='red'>小青蛙</span>"
    $($html).appendTo("div");
</script>
```

before()和after()方法可以在元素的前后插入内容

```javascript
<script type="text/javascript">
    var $html = "<span class='red'>兄弟。</span>"
    $("span").after($html);
</script>
```

clone()方法可以生成一个被选元素的副本，即复制了一个被选元素，包含它的节点、文本和属性，它的调用格式为：

```javascript
$(selector).clone()
```

replaceWith()和replaceAll()方法都可以用于替换元素或元素中的内容，但它们调用时，内容和被替换元素所在的位置不同，分别为如下所示：

```javascript
$(selector).replaceWith(content)
$(content).replaceAll(selector)
```


