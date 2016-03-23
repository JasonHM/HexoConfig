title: JQuery基础
date: 2015-10-22 10:52:55
tags: jquery
---

个人理解: jQuery是对js的一层封装，将需要写很多javascript代码的功能给封装成简单的函数。有特性（链式操作，行为层和结构层的分离..）,入门门槛低。

<!-- more -->。<!-- more -->

## 基础选择器

- id
- element
- .class
- *
- sele1,sele2,seleN
- ance desc 
- parent child
- prev nd()+ next 
- prev ~ siblings

`$("parent allChildren")` `parent`下所有的`child`元素
`$("parent>child")` `parent`第一代的`child`元素
`$("prev+next")` `prev`紧挨着且匹配的唯一元素
`e("prev~next")` `prev`之后着且匹配的多个元素
    
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
wrap()和wrapInner()方法都可以进行元素的包裹，但前者用于包裹元素本身，后者则用于包裹元素中的内容，它们的调用格式分别为：

```javascript
$(selector).wrap(wrapper)和$(selector).wrapInner(wrapper)
```

```javascript
<script type="text/javascript">
    $(".red").wrapInner("<em></em>");
</script>
```
each()方法可以遍历指定的元素集合，在遍历时，通过回调函数返回遍历元素的序列号，它的调用格式为：
```javascript
$(selector).each(function(index))
```
```javascript
<script type="text/javascript">
$("span").each(function (index) {
    if (index == 1) {
        $(this).attr("class", "red");
    }
});
</script>
```
参数function为遍历时的回调函数，index为遍历元素的序列号，它从0开始。

remove()方法删除所选元素本身和子元素，该方法可以通过添加过滤参数指定需要删除的某些元素，而empty()方法则只删除所选元素的子元素。

## jQuery 事件与应用

ready()事件类似于onLoad()事件，但前者只要页面的DOM结构加载后便触发，而后者必须在页面全部元素加载成功才触发
```javascript
$(document).ready(function(){
    $("#btntest").bind("click", function () {
    $("#tip").html("我被点击了！");
    });
});
             
```
bind()方法绑定元素的事件非常方便，绑定前，需要知道被绑定的元素名，绑定的事件名称，事件中执行的函数内容就可以，它的绑定格式如下：

```javascript
$(selector).bind(event,[data] function)
```
```
<script type="text/javascript">
$(function () {
    $("#btntest").bind("click mouseout", function () {
        $(this).attr("disabled", "true");
    })
});
</script>
```
hover()方法的功能是当鼠标移到所选元素上时，执行方法中的第一个函数，鼠标移出时，执行方法中的第二个函数，实现事件的切实效果，调用格式如下：
```
$(selector).hover(over，out);
```
```
<script type="text/javascript">
    $(function (){
        $("div").hover(
            function () {
                $(this).addClass("orange");
            },
            function () {
                $(this).removeClass("orange")
            }
        )
    });
</script>
```
toggle()方法可以在元素的click事件中绑定两个或两个以上的函数，同时，它还可以实现元素的隐藏与显示的切换，绑定多个函数的调用格式如下：
```
$(selector).toggle(fun1(),fun2(),funN(),...)
```
unbind()方法可以移除元素已绑定的事件，它的调用格式如下：

```
$(selector).unbind(event,fun)
```
其中参数event表示需要移除的事件名称，多个事件名用空格隔开，fun参数为事件执行时调用的函数名称。如果没有规定参数，unbind() 方法会删除指定元素的所有事件处理程序

one()方法可以绑定元素任何有效的事件，但这种方法绑定的事件只会触发一次，它的调用格式如下：
```
$(selector).one(event,[data],fun)
```
参数event为事件名称，data为触发事件时携带的数据，fun为触发该事件时执行的函数。

trigger()方法可以直接手动触发元素指定的事件，这些事件可以是元素自带事件，也可以是自定义的事件，总之，该事件必须能执行，它的调用格式为：

```
$(selector).trigger(event)
```
focus事件在元素获取焦点时触发，如点击文本框时，触发该事件；而blur事件则在元素丢失焦点时触发，如点击除文本框的任何元素，都会触发该事件。
```
<script type="text/javascript">
$(function () {
    $("input")
    .bind("focus", function () {
        $("div").html("请输入您的姓名！");
    })
    .bind("blur", function () {
        if ($(this).val().length == 0)
            $("div").html("你的名称不能为空！");
        })
    });
</script> 
```
当一个元素的值发生变化时，将会触发change事件

与bind()方法相同，live()方法与可以绑定元素的可执行事件，除此相同功能之外，live()方法还可以绑定动态元素，即使用代码添加的元素事件，格式如下：
```
$(selector).live(event,[data],fun)
```
参数event为事件名称，data为触发事件时携带的数据，fun为触发该事件时执行的函数。
注意：从 jQuery 1.7 开始，不再建议使用 .live() 方法。1.9不支持.live()

## jQuery 动画特效

show()和hide()方法用于显示或隐藏页面中的元素，它的调用格式分别为：
```
$(selector).hide(speed,[callback])和$(selector).show(speed,[callback])
```
参数speed设置隐藏或显示时的速度值，可为“slow”、“fast”或毫秒数值(如:3000)，可选项参数callback为隐藏或显示动作执行完成后调用的函数名。

toggle()方法以动画的效果显示和隐藏元素
```
$(selector).toggle(speed,[callback])
```
其中speed参数为动画效果时的速度值，可以为数字，单位为毫秒，也可是“fast”、“slow”字符，可选项参数callback为方法执行成功后回调的函数名称。

slideUp()和slideDown()方法在页面中滑动元素，前者用于向上滑动元素，后者用于向下滑动元素，它们的调用方法分别为：
```
$(selector).slideUp(speed,[callback])和$(selector).slideDown(speed,[callback])
```
其中speed参数为滑动时的速度，单位是毫秒，可选项参数callback为滑动成功后执行的回调函数名。
要注意的是：slideDown()仅适用于被隐藏的元素；slideup()则相反。

slideToggle()方法可以切换slideUp()和slideDown()，即调用该方法时，如果元素已向上滑动，则元素自动向下滑动，反之，则元素自动向上滑动，格式为：
```
$(selector).slideToggle(speed,[callback])
```
其中speed参数为动画效果时的速度值，可以为数字，单位为毫秒，也可是“fast”、“slow”字符，可选项参数callback为方法执行成功后回调的函数名称。

fadeIn()和fadeOut()方法可以实现元素的淡入淡出效果，前者淡入隐藏的元素，后者可以淡出可见的元素，它们的调用格式分别为：
```
$(selector).fadeIn(speed,[callback])和$(selector).fadeOut(speed,[callback])
```
其中参数speed为淡入淡出的速度，callback参数为完成后执行的回调函数名。

fadeTo()方法，可以将所选择元素的不透明度以淡入淡出的效果调整为指定的值，该方法的调用格式为：
```
$(selector).fadeTo(speed,opacity,[callback])
```
其中speed参数为效果的速度，opacity参数为指定的不透明值，它的取值范围是0.0~1.0，可选项参数callback为效果完成后，回调的函数名。

animate()方法可以创建自定义动画效果，它的调用格式为：

```
$(selector).animate({params},speed,[callback])
```
其中，params参数为制作动画效果的CSS属性名与值，speed参数为动画的效果的速度，单位为毫秒，可选项callback参数为动画完成时执行的回调函数名。
```
<script type="text/javascript">
    $(function () {
        $("span").animate({
            width: "80px",
            height: "80px"
        },
        3000, function () {
            $("#tip").html("执行完成!");
        });
    });
</script>
```
```
<script type="text/javascript">
    $(function () {
        $("span").animate({
            left: "+=100px"
        }, 3000, function () {
            $(this).animate({
                height: '+=30px',
                width: '+=30px'
            }, 3000, function () {
                $("#tip").html("执行完成!");
            });
        });
    });
</script>
```
stop()方法的功能是在动画完成之前，停止当前正在执行的动画效果，这些效果包括滑动、淡入淡出和自定义的动画，它的调用格式为：

```
$(selector).stop([clearQueue],[goToEnd])
```
其中，两个可选项参数clearQueue和goToEnd都是布尔类型值，前者表示是否停止正在执行的动画，后者表示是否完成正在执行的动画，默认为false。

delay()方法的功能是设置一个延时值来推迟动画效果的执行，它的调用格式为：
```
$(selector).delay(duration)
```
其中参数duration为延时值，它的单位是毫秒，当超过延时值时，动画继续执行。

## jQuery 实现Ajax应用

使用load()方法异步请求数据
load()方法通过Ajax请求加载服务器中的数据，并把返回的数据放置到指定的元素中，它的调用格式为：
```
load(url,[data],[callback])
```
参数url为加载服务器地址，可选项data参数为请求时发送的数据，callback参数为数据请求成功后，执行的回调函数。
```
<script type="text/javascript">
    $(function () {
        $("#btnShow").bind("click", function () {
            var $this = $(this);
            $("ul")
            .html("<img src='Images/Loading.gif' alt=''/>")
            .load("http://www.imooc.com/data/fruit_part.html",function(){
                $this.attr("disabled", "true");
            });
        })
    });
</script>
```

getJSON()方法可以通过Ajax异步请求的方式，获取服务器中的数组，并对获取的数据进行解析，显示在页面中，它的调用格式为：
```
jQuery.getJSON(url,[data],[callback])或$.getJSON(url,[data],[callback])
```
```
<script type="text/javascript">
    $(function () {
        $("#btnShow").bind("click", function () {
            var $this = $(this);
            $.getJSON("http://www.imooc.com/data/sport.json",function(data){
                $this.attr("disabled", "true");
                $.each(data, function (index, sport) {
                    if(index==3)
                        $("ul").append("<li>" + sport["name"] + "</li>");
                });
            });
        })
    });
</script>
```
其中，url参数为请求加载json格式文件的服务器地址，可选项data参数为请求时发送的数据，callback参数为数据请求成功后，执行的回调函数。

getScript()方法异步请求并执行服务器中的JavaScript格式的文件，它的调用格式如下所示：
```
jQuery.getScript(url,[callback])或$.getScript(url,[callback])
```
参数url为服务器请求地址，可选项callback参数为请求成功后执行的回调函数。

get()方法时，采用GET方式向服务器请求数据，并通过方法中回调函数的参数返回请求的数据，它的调用格式如下：
```
$.get(url,[callback])
```
参数url为服务器请求地址，可选项callback参数为请求成功后执行的回调函数。

serialize()方法可以将表单中有name属性的元素值进行序列化，生成标准URL编码文本字符串，直接可用于ajax请求，它的调用格式如下：
```
$(selector).serialize()
```
其中selector参数是一个或多个表单中的元素或表单元素本身。

ajax()方法是最底层、功能最强大的请求服务器数据的方法，它不仅可以获取服务器返回的数据，还能向服务器发送请求并传递数值，它的调用格式如下：
```
jQuery.ajax([settings])或$.ajax([settings])
```
```
<script type="text/javascript">
    $(function () {
        $("#btnCheck").bind("click", function () {
            $.ajax({
                url: "http://www.imooc.com/data/check.php",
                data: { num: $("#txtNumber").val()  },
                type: "POST",
                success: function (data) {
                    $("ul").append("<li>你输入的<b>  "
                    + $("#txtNumber").val() + " </b>是<b> "
                    + data + " </b></li>");
                }
            });
        })
    });
</script>
```
其中参数settings为发送ajax请求时的配置对象，在该对象中，url表示服务器请求的路径，data为请求时传递的数据，dataType为服务器返回的数据类型，success为请求成功的执行的回调函数，type为发送数据请求的方式，默认为get。

ajaxStart()和ajaxStop()方法是绑定Ajax事件。ajaxStart()方法用于在Ajax请求发出前触发函数，ajaxStop()方法用于在Ajax请求完成后触发函数。它们的调用格式为：

```
$(selector).ajaxStart(function())和$(selector).ajaxStop(function())
```
```
jQuery.ajaxSetup([options])或$.ajaxSetup([options])
```
可选项options参数为一个对象，通过该对象设置Ajax请求时的全局选项值。

使用ajaxStart()和ajaxStop()方法

## jQuery 常用插件

表单验证插件——validate
该插件自带包含必填、数字、URL在内容的验证规则，即时显示异常信息，此外，还允许自定义验证规则，插件调用方法如下：
```
$(form).validate({options})
```
其中form参数表示表单元素名称，options参数表示调用方法时的配置对象，所有的验证规则和异常信息显示的位置都在该对象中进行设置。

表单插件——form
通过表单form插件，调用ajaxForm()方法，实现ajax方式向服务器提交表单数据，并通过方法中的options对象获取服务器返回数据，调用格式如下：
```
$(form). ajaxForm ({options})
```
```
<script type="text/javascript">
    $(function () {
        var options = {
            url: "http://www.imooc.com/data/form_f.php", 
            target: ".tip"
        }
        $("#frmV").ajaxForm(options);
    });
</script>
```
其中form参数表示表单元素名称；options是一个配置对象，用于在发送ajax请求过程，设置发送时的数据和参数。

图片灯箱插件——lightBox
该插件可以用圆角的方式展示选择中的图片，使用按钮查看上下张图片，在加载图片时自带进度条，还能以自动播放的方式浏览图片，调用格式如下：
```
$(linkimage).lightBox({options})
```
其中linkimage参数为包含图片的<a>元素名称，options为插件方法的配置对象。</a>

图片放大镜插件——jqzoom
在调用jqzoom图片放大镜插件时，需要准备一大一小两张一样的图片，在页面中显示小图片，当鼠标在小图片中移动时，调用该插件的jqzoom()方法，显示与小图片相同的大图片区域，从而实现放大镜的效果，调用格式如下：
```
$(linkimage).jqzoom({options})
```
```
<script type="text/javascript">
    $(function () {
        $("#jqzoom").jqzoom({ //绑定图片放大插件jqzoom
            zoomWidth: 123, //小图片所选区域的宽
            zoomHeight: 123, //小图片所选区域的高
            zoomType: 'reverse' //设置放大镜的类型
        });
    });
</script>
```

其中linkimage参数为包含图片的<a>元素名称，options为插件方法的配置对象。</a>

cookie插件——cookie
使用cookie插件后，可以很方便地通过cookie对象保存、读取、删除用户的信息，还能通过cookie插件保存用户的浏览记录，它的调用格式为：

保存：$.cookie(key，value)；读取：$.cookie(key)，删除：$.cookie(key，null)

其中参数key为保存cookie对象的名称，value为名称对应的cookie值。

搜索插件——autocomplete
搜索插件的功能是通过插件的autocomplete()方法与文本框相绑定，当文本框输入字符时，绑定后的插件将返回与字符相近的字符串提示选择，调用格式如下：
```
$(textbox).autocomplete(urlData,[options]);
```
其中，textbox参数为文本框元素名称，urlData为插件返回的相近字符串数据，可选项参数options为调用插件方法时的配置对象。


右键菜单插件——contextmenu
右键菜单插件可以绑定页面中的任意元素，绑定后，选中元素，点击右键，便通过该插件弹出一个快捷菜单，点击菜单各项名称执行相应操作，调用代码如下：
```
$(selector).contextMenu(menuId,{options});
```
```
<script type="text/javascript">
    $(function () {
        $("#btnSubmit").contextMenu("sysMenu",
        { bindings:
            {
                'Li3': function (Item) {
                    $(".tip").show().html("您点击了“保存”项");
                },
                'Li4': function (Item) {
                    $(".tip").show().html("您点击了“退出”项");
                }
            }
        });
    });
</script>
```
Selector参数为绑定插件的元素，meunId为快捷菜单元素，options为配置对象。

自定义对象级插件——lifocuscolor插件

自定义的lifocuscolor插件可以在<ul>元素中，鼠标在表项<li>元素移动时，自定义其获取焦点时的背景色，即定义<li>元素选中时的背景色，调用格式为：
```
$(Id).focusColor(color)
```
```
<script type="text/javascript">
    $(function () {
        $("#u1").focusColor("#ccc"); //调用自定义的插件
    })
</script>
```
其中，参数Id表示<ul>元素的Id号，color表示<li>元素选中时的背景色。

自定义类级别插件—— twoaddresult

通过调用自定义插件twoaddresult中的不同方法，可以实现对两个数值进行相加和相减的运算，导入插件后，调用格式分别为：
```
$.addNum(p1,p2) 和 $.subNum(p1,p2)
```
上述调用格式分别为计算两数值相加和相减的结果，p1和p2为任意数值。

## jQuery UI型插件

拖曳插件——draggable
拖曳插件draggable的功能是拖动被绑定的元素，当这个jQuery UI插件与元素绑定后，可以通过调用draggable()方法，实现各种拖曳元素的效果，调用格式如下：
```
$(selector). draggable({options})
```
options参数为方法调用时的配置对象，根据该对象可以设置各种拖曳效果，如“containment”属性指定拖曳区域，“axis”属性设置拖曳时的坐标方向。

放置插件——droppable
除使用draggable插件拖曳任意元素外，还可以调用droppable UI插件将拖曳后的任意元素放置在指定区域中，类似购物车效果，调用格式如下：
```
$(selector).droppable({options})
```
selector参数为接收拖曳元素，options为方法的配置对象，在对象中，drop函数表示当被接收的拖曳元素完全进入接收元素的容器时，触发该函数的调用。

拖曳排序插件——sortable
拖曳排序插件的功能是将序列元素（例如<option>、<li>）按任意位置进行拖曳从而形成一个新的元素序列，实现拖曳排序的功能，它的调用格式为：
```
$(selector).sortable({options});
```
selector参数为进行拖曳排序的元素，options为调用方法时的配置对象，</li></option>

面板折叠插件——accordion
面板折叠插件可以实现页面中指定区域类似“手风琴”的折叠效果，即点击标题时展开内容，再点另一标题时，关闭已展开的内容，调用格式如下：
```
$(selector).accordion({options});
```
其中，参数selector为整个面板元素，options参数为方法对应的配置对象。

选项卡插件——tabs

使用选项卡插件可以将<ul>中的<li>选项定义为选项标题，在标题中，再使用<a>元素的“href”属性设置选项标题对应的内容，它的调用格式如下：
```
$(selector).tabs({options});
```
selector参数为选项卡整体外围元素，该元素包含选项卡标题与内容，options参数为tabs()方法的配置对象，通过该对象还能以ajax方式加载选项卡的内容。</a></li></ul>

对话框插件——dialog

对话框插件可以用动画的效果弹出多种类型的对话框，实现JavaScript代码中alert()和confirm()函数的功能，它的调用格式为：
```
$(selector).dialog({options});
```
selector参数为显示弹出对话框的元素，通常为<div>，options参数为方法的配置对象，在对象中可以设置对话框类型、“确定”、“取消”按钮执行的代码等。</div>


菜单工具插件——menu

菜单工具插件可以通过<ul>创建多级内联或弹出式菜单，支持通过键盘方向键控制菜单滑动，允许为菜单的各个选项添加图标，调用格式如下：
```
$(selector).menu({options});
```
selector参数为菜单列表中最外层<ul>元素，options为menu()方法的配置对象。

微调按钮插件——spinner

微调按钮插件不仅能在文本框中直接输入数值，还可以通过点击输入框右侧的上下按钮修改输入框的值，还支持键盘的上下方向键改变输入值，调用格式如下：
```
$(selector).spinner({options});
```
selector参数为文本输入框元素，可选项options参数为spinner()方法的配置对象，在该对象中，可以设置输入的最大、最小值，获取改变值和设置对应事件。

工具提示插件——tooltip

工具提示插件可以定制元素的提示外观，提示内容支持变量、Ajax远程获取，还可以自定义提示内容显示的位置，它的调用格式如下：
```
$(selector).tooltip({options});
```
其中selector为需要显示提示信息的元素，可选项参数options为tooltip()方法的配置对象，在该对象中，可以设置提示信息的弹出、隐藏时的效果和所在位置。

## jQuery 工具类函数

获取浏览器的名称与版本信息
在jQuery中，通过$.browser对象可以获取浏览器的名称和版本信息，如$.browser.chrome为true，表示当前为Chrome浏览器，$.browser.mozilla为true，表示当前为火狐浏览器，还可以通过$.browser.version方式获取浏览器版本信息。
```
<script type="text/javascript">
$(function () {
    var strTmp = "您的浏览器名称是：";
   if ($.browser.chrome) { //谷歌浏览器
        strTmp += "Chrome";
   }
   if ($.browser.mozilla) { //火狐相关浏览器
        strTmp += "Mozilla FireFox";
   }
   strTmp += "<br /><br /> 版本号是：" //获取版本号
   +$.browser.version;
   $(".content").html(strTmp);
});
</script>
```
检测浏览器是否属于W3C盒子模型
浏览器的盒子模型分为两类，一类为标准的w3c盒子模型，另一类为IE盒子模型，两者区别为在Width和Height这两个属性值中是否包含padding和border的值，w3c盒子模型不包含，IE盒子模型则包含，而在jQuery 中，可以通过$.support.boxModel对象返回的值，检测浏览器是否属于标准的w3c盒子模型。
```
<script type="text/javascript">
$(function () {
    var strTmp = "您打开的页面是：";
    if ($.support.boxModel) { //是W3C盒子模型
        strTmp += "W3C盒子模型";
    }
    else { //是IE盒子模型
        strTmp += "IE盒子模型";
    }
    $(".content").html(strTmp);
});
</script>
```
检测对象是否为空
在jQuery中，可以调用名为$.isEmptyObject的工具函数，检测一个对象的内容是否为空，如果为空，则该函数返回true，否则，返回false值，调用格式如下：
```
$.isEmptyObject(obj);
```
其中，参数obj表示需要检测的对象名称。

检测对象是否为原始对象
调用名为$.isPlainObject的工具函数，能检测对象是否为通过{}或new Object()关键字创建的原始对象，如果是，返回true，否则，返回false值，调用格式为：
```
$.isPlainObject (obj);
```
ns的工具函数，能检测在一个DOM节点中是否包含另外一个DOM节点，如果包含，返回true，否则，返回false值，调用格式为：
```
$.contains (container, contained)其中，参数obj表示需要检测的对象名称。
```
检测两个节点的包含关系

调用名为$.contains的工具函数，能检测在一个DOM节点中是否包含另外一个DOM节点，如果包含，返回true，否则，返回false值，调用格式为：
```
$.contains (container, contained);
```
参数container表示一个DOM对象节点元素，用于包含其他节点的容器，contained是另一个DOM对象节点元素，用于被其他容器所包含。


字符串操作函数

调用名为$.trim的工具函数，能删除字符串中左右两边的空格符，但该函数不能删除字符串中间的空格，调用格式为：
```
$.trim (str);
```
参数str表示需要删除左右两边空格符的字符串。

URL操作函数

调用名为$. param的工具函数，能使对象或数组按照key/value格式进行序列化编码，该编码后的值常用于向服务端发送URL请求，调用格式为：
```
$. param (obj);
```
参数obj表示需要进行序列化的对象，该对象也可以是一个数组，整个函数返回一个经过序列化编码后的字符串。

使用$.extend()扩展工具函数
调用名为$. extend的工具函数，可以对原有的工具函数进行扩展，自定义类级别的jQuery插件，调用格式为：
```
$. extend ({options});
```
参数options表示自定义插件的函数内容。
```
<script type="text/javascript">
            /*------------------------------------------------------------/
            功能：返回两个数中最小值
            参数：数字p1,p2
            返回：最小值的一个数
            示例：$.MinNum(1,2);
            /------------------------------------------------------------*/
(function ($) {
    $.extend({
        "MinNum": function (p1, p2) {
            return (p1 > p2) ? p2 : p1;
        }
    });
})(jQuery);
$(function () {
    $("#btnShow").bind("click", function () {
        $(".tip").html("");
        var strTmp = "17与18中最小的数是：";
        strTmp +=$.MinNum(17, 18);
        //显示在页面中
        $(".tip").show().append(strTmp);
    });
});
</script>
```
使用$.extend()扩展Object对象

除使用$.extend扩展工具函数外，还可以扩展原有的Object对象，在扩展对象时，两个对象将进行合并，当存在相同属性名时，后者将覆盖前者，调用格式为：
```
$. extend (obj1,obj2,…objN);
```
参数obj1至objN表示需要合并的各个原有对象。

## jQuery在线聊天室
聊天室基本功能介绍 (02:35)
聊天室案例页面效果展示 (09:00)
聊天室数据流程分析 (03:32)
登录页面开发 (15:21)
聊天室主页代码功能分析 (05:50)
简短回顾聊天主页的功能 (01:46)
“发送”按钮代码功能解析 (05:56)
“表情图标”的添加代码分析 (06:17)
点击“表情图标”时的事件代码说明 (03:47)
定时获取聊天内容和在线人员信息的功能实现 (06:54)
通过页面元素侦察Ajax请求过程的状态 (02:21)
