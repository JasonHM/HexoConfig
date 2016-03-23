# HTML5笔记

##全局属性:

data-example: 自定义的属性,example为自己定义的

hidden: 隐藏标签元素

spellcheck: 对输入内容进行语法纠错

tabindex: 使用tab键时,焦点的跳转顺序

contentediable: 将控件内容能够进行局部修改

```
//全局内容修改
<script>
	window.document.designMode = 'on';
</script>
```

##增加标签：

###结构标签

- section：独立内容区块，可以用h1~h6组成大纲，表示文档结构，也可以有章节、页眉、页脚或页眉的其他部分；
- article：特殊独立区块，表示这篇页眉中的核心内容；
- aside：标签内容之外与标签内容相关的辅助信息；
- header：某个区块的头部信息/标题；
- hgroup：头部信息/标题的补充内容；
- footer：底部信息；
- nav： 导航栏
- figure：独立的单元，例如某个有图片与内容的新闻块。

###表单标签

- email：必须输入邮件；
- url：必须输入url地址；
- number：必须输入数值；
- range：必须输入一定范围内的数值；
- Date Pickers：日期选择器；
	- date：选取日、月、年
	- month：选取月、年
	- week：选取周和年
	- time：选取时间（小时和分钟）
	- datetime：选取时间、日、月、年（UTC时间）
	- datetime-local：选取时间、日、月、年（本地时间）
- search：搜索常规的文本域；
- color
 
###媒体标签

- video：视频
- audio：音频
- embed：嵌入内容（包括各种媒体），Midi、Wav、AU、MP3、Flash、AIFF等。

###其他功能标签

- mark：标注（像荧光笔做笔记）
- progress：进度条；

	```
	<progress max="最大进度条的值" value="当前进度条的值">
	```

- time：数据标签，给搜索引擎使用；
	- 发布日期

	```
	<time datetime="2014-12-25T09:00">9：00</time>
	```
	
	- 更新日期:

	```
	<time datetime="2015-01-23T04:00" pubdate>4:00</time>
	```
- ruby和rt：对某一个字进行注释； `<ruby><rt>` 注释内容 `</rt><rp>`浏览器不支持时如何显示</rp></ruby>
- wbr：软换行，页面宽度到需要换行时换行；
- canvas：使用JS代码做内容进行图像绘制；
- command：按钮；
- deteils ：展开菜单；
- dateilst：文本域下拉提示；
- keygen:加密；