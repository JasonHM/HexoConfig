title: 精通css第二版读书笔记
date: 2016-07-01
tags: 
    - css
categories: 编程

---
本篇内容：
    将自己在读这本书时自己不清楚或不知道的内容记录下来.
    
<!--more-->  

## 第二章: 为样式找到应用目标

元素选择器 ID选择器 Class选择器 通用选择器
### 伪类选择器 

链接伪类:link :visited,用于锚元素
动态伪类 :active :hover :focus
 IE6 应用于锚链接的:active和:hover选择器 忽略:focus,
 IE7 任何元素支持:hover,忽略 :active :focus

// 例子: 已访问链接和未访问链接鼠标悬停效果
```
a:visited:hover{color: olive}
```

### 高级选择器

子选择器,如 `ul > li`
IE7和高于其版本的都支持,在父类和子类之间有注释会产生BUG
IE6可以通过通用选择器模拟子选择器效果

相邻元素选择器, 如 `h2 + p`,指h2并列的第一个p标签

属性选择器,IE7及其以上支持
p[title]
p[title]:hover

IE6不支持属性选择器
可以通过下面的方式设置两种不通浏览器的风格

```
#header{
    background: url(branding_bw.png) repeat-y left top;
}
[id="header"]{
    background: url(branding_color.png)  repeat-y left top;
}
```

层叠

- 标有!important的用户样式
- 标有!important的作者样式
- 作者样式
- 用户样式
- 浏览器/用户代理应用的样式


选择器优先级,特殊性

| 选择器  | 特殊性(a,b,c,d)   | 以10为基数的特殊性  |
 ---- | ---- | ----
| Style="" | 1,0,0,0 | 1000 |
| #wrapper #content{} | 0,2,0,0 | 200 |
| #content .datePosted{} | 0,1,1,0 | 110 |
| div#content | 0,1,0,1 | 101 |
| #content | 0,1,0,0 | 100 |
| p.comment .dateposted{} | 0,0,2,1 | 21 |
| p.comment{} | 0,0,1,1 | 11 |
| div p{} | 0,0,0,2 | 2 |
| p{} | 0,0,0,1 | 1 |

- a = 行内样式
- b = ID选择器总数
- c = 类，伪类，属性选择器的总数
- d = 类型选择器和伪类选择器的数量

文档样式分割，但下面这种方式导入样式比链接样式表慢，影响下载时间，而且老式浏览器对于同时传输的文件数量有要求，所以更倾向于单一样式表而不是多个小文件。

```
/* css文件间可以使用import导入其他样式表 */
@import url(/css/layout.css)
```

在单一样式表中分割可以使用下面的注释来区分不同的模块

```
/* @group typography */
```

这样通过搜索`@group typ`就能够快速的定位了

样式文本结构如下:

- 一般性样式 `* @group gemeral styles`
    - 主体样式
    - reset样式
    - 链接
    - 标题
    - 其他元素
- 辅助样式 `@group helper styles`
    - 表单
    - 通知和错误
    - 一致的条目
- 页面结构 `@group page structure`
    - 标题，页脚，导航
    - 布局
    - 其他页面结构
- 页面组件 `@group page components`
    - 各个页面
- 覆盖 ``@group overrides

@todo 需要修改，复查的代码
@bugfix 表示代码或特定浏览器遇到的问题
@workaround 不完善的权益之计

### 第三章 可视化格式模型

inline-block:   让元素能够像行内（inline）元素一样排列，内容符合块级框（block）的行为，能够设置高度，宽度,垂直外边距

P44