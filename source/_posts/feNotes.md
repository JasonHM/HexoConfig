title: 前端开发笔记
date: 2016-01-28
tags: 
    - javascript
    - html
categories: 编程

---
  
## 封装部分的html code重复使用: 
<!--more-->

### [load](http://api.jquery.com/load/)

```html
<!doctype html>
<head>
  <meta charset="utf-8">
  <title>load demo</title>
  <script src="https://code.jquery.com/jquery-1.10.2.js"></script>
</head>
<body>
 
<div id="testLoad"></div>
 
<script>
$("#testLoad").load("/resources/load.html");
</script>
 
</body>
</html>
```

### [imports](http://www.html5rocks.com/zh/tutorials/webcomponents/imports/)

warnings.html:

```html
<div class="warning">
  <style scoped>
    h3 {
      color: red;
    }
  </style>
  <h3>Warning!</h3>
  <p>This page is under construction</p>
</div>

<div class="outdated">
  <h3>Heads up!</h3>
  <p>This content may be out of date</p>
</div>
```

在index.html中复制一部分waring代码过来: 

```html
<head>
  <link rel="import" href="warnings.html">
</head>
<body>
  <script>
    var link = document.querySelector('link[rel="import"]');
    var content = link.import;

    // 从 warning.html 的文档中获取 DOM。
    var el = content.querySelector('.warning');

    document.body.appendChild(el.cloneNode(true));
  </script>
</body>
```

### [react](http://stackoverflow.com/questions/22461129/switch-class-on-tabs-with-react-js)写一个模块

下面是我写的一个例子: 
```
var React = require('react');

var TabComponent = React.createClass({
    getInitialState: function() {
        return {
            activeMenuItemTitle: 'Home'
        };
    },
    setActiveMenuItem: function(title) {
        this.setState({
            activeMenuItemTitle: title
        });
    },
    render: function() {
        var menuItems = this.props.data.map(function(menuItem) {
            return (
                <MenuItem active={this.state.activeMenuItemTitle === menuItem.title} key= {menuItem.title} onSelect= {this.setActiveMenuItem} title= {menuItem.title} href={menuItem.href}/>
            );
        }.bind(this));
        return (
            <ul className="nav nav-tabs" >
                {menuItems}
            </ul>
        );
    }
});

var MenuItem = React.createClass({
    handleClick: function(event) {
        //event.preventDefault();
        this.props.onSelect(this.props.title);
    },
    render: function() {
        var className = this.props.active ? 'active' : "";
        return (
            <li className={className} >
                <a href={this.props.href} onClick={this.handleClick} >{this.props.title}</a>
            </li>
        );
    }
});

module.exports = TabComponent;
```

## Ajax中的跨域请求

在使用ajax添加headers的过程中,方法很简单。[（解决方法）](http://stackoverflow.com/questions/3258645/pass-request-headers-in-a-jquery-ajax-get-call)。第一次写，没什么经验。一直以为是我的ajax的参数有问题。后台也太懂,还上stackoverflow提问，结果还被点了个负分。后面查到资料是需要后台开放请求头,这时候的自定义的请求才能够到达。如何请求的过程[在这](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Access_control_CORS#Access-Control-Request-Headers),用自己的话说就是:
  
  - 小弟: 老大，我想要点东西（OPTIONS 发送一个预请求）
  - 老大: 瞅一下,（匹配通过）是我的小弟。嗯, 你说吧!
  - 小弟: 单子在这呢,您看一下(POST GET 请求)
  - 老大: 看在你平时孝敬我的份上,这批货就给你了(返回数据)

## Ajax请求的封装

第一次写前端,后面遇到要给自己的每一个请求头(headers)都加上一组{key: value},一开始写的是直接将$.ajax请求包裹起来,用一个方法代替,如下:

```javascript
function publicAjax(args) {
    $.ajax({
        "url": args.url,
        "dataType": 'json',
        type: args.type || 'GET',
        data: args.data || '',
        xhrFields: {
            withCredentials: true
        },
        "success": function(data) {
            if (data.token) {
                setToken(data.token);
            }
            args.success(data);
        },
        "error": function() {
            alert("网络状况不好，请重试");
        }
    });
}
```
后来由于这个方法有局限性,不适用于某些插件(如:[datables](https://www.datatables.net/)),找到一种更好的方法。主要用到的jquery的`$.extend`方法,代码如下:

```
(function($) {
        //备份jquery的ajax方法  
        var _ajax = $.ajax;

        //重写jquery的ajax方法  
        $.ajax = function(opt) {
            //备份opt中error和success方法  
            var fn = {
                error: function(XMLHttpRequest, textStatus, errorThrown) {},
                success: function(data, textStatus) {}
            }
            if (opt.error) {
                fn.error = opt.error;
            }
            if (opt.success) {
                fn.success = opt.success;
            }

            //扩展增强处理  
            var _opt = $.extend(opt, {
                beforeSend: function(req) {
                    //req.setRequestHeader("mark", getToken());
                },
                error: function(xmlhttprequest, textstatus, errorthrown) {
                    switch (xmlhttprequest.status) {

                    }
                    //错误方法增强处理
                    fn.error(xmlhttprequest, textstatus, errorthrown);
                },
                success: function(data, textStatus, xhr) {
                    //成功回调方法增强处理  
                    fn.success(data, textStatus);
                },
                complete: function(XMLHttpRequest, textStatus) {

                },
            });
            _ajax(_opt);
        };
    })(jQuery);
```
解决的大部分的问题请求加上{key: value}的问题。看到这里的同学可以不要往下看了,下面的跟这个问题没有很大关联,只是记录我的一些问题。然而新的问题就是一些header的问题了。这种封装情况下:

```
xhrFields: {
    withCredentials: true
},
```
这个属性在上面函数的beforeSend中加并没有效果，使ResquestHeaders中的Cookie丢失了,只有将在外部的$.ajax参数中了。本想获取cookie值来手动添加的，后面查到文档中有一些自定义的header是不允许添加的。[详情查看](https://dvcs.w3.org/hg/xhr/raw-file/tip/Overview.html#dom-xmlhttprequest-setrequestheader)。 最后只有妥协,第一种和第二种方法都共用。


## 解析XML（广度优先算法）

上课的时候没有认真听,只有点影响,觉得二叉树、广度优先算法、深度优先算法都很高大上的感觉。由于有一个地址的需求,然后我就的硬着头皮去看。后面终于明白了这个东西,还是比较能够理解的嘛！

如下面一段xml表格:

```xml
<g id="11" name="中国">
    <p id="01" name="北京">
        <c id="01" name="朝阳">
        <c id="02" name="海淀">
    </p>
    <p id="02" name="天津">
        <c id="01" name="南开">
        <c id="02" name="河西">
    </p>
</g>
```
目标: 我需要找到`南开`:

- 普通查询: 中国 -> 北京 -> 朝阳 -> 海淀 -> 天津 -> 南开

- 我想要的查询路径: 中国 -> 天津 -> 南开

如何才能做的到呢,这时候就用到了id这个属性,我所查询的河西等于110201的编号。既定的存储规则为国家11-99标示,站字节前两位;省为0-99区间,站中间两位;市区站后面两位0-99的规则。

此时我查询的步骤是先查所有国家中id为11的国家找到中国,然后查询`中国`下面所有`id`为`02`的省,得到`天津`;最后查询天津下面`id`为02的市区,得到`南开`。

这就是我所理解的广度优先算法了,先查一级目录,然后二级目录,三级目录...
