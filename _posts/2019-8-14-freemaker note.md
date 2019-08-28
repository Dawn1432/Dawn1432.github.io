---
layout: post
title: freemaker笔记
date: 2019-08-14
tags: experience_note
---
### 概述

<p>作为一个服务器开发，理论上来讲前端和后端的东西都得懂一点。我之前的公司（学校实验室）的前端是用jsp+js来做的，而现在这边的前端则大部分是用html+freemaker来做的。那学习freemaker语法自然也就成了工作的一部分。</p>
<p>刚开始看到.ftl文件后缀的时候是懵逼的，对于这种前端的数据交互和处理毫无头绪，后来知道这个是叫freemaker在简单看了一些用户手册之后，现阶段算是差不多能做一些基本操作了，这里对自己感觉比较重要的部分做一个记录，以供后续查阅。</p>
<p>反正这种东西给我的感觉是，必须结合view来进行model处理，虽然比较符合springMVC的那种思想，但是总感觉看起来不太高级的亚子，不知道以后会不会对他有所改观。</p>
<img src='https://dawn1432.github.io\images\freemaker笔记\你怎么这个亚子.png' align='margin-left' style=' width:170px;height:150px;margin:0;'/><br>

### 正文

## 数据模型

哈希表->作为目录的变量(目前还没用过)<br>
标量(Scalars)->存储单值的变量<br>
序列(sequences)->列表<br>

标量类型<br>
字符串，数字，日期/时间，布尔值<br>

## 特殊代码段：
插值(interpolation)：${...}<br>
FTL 标签/指令: # 开头。自定义的用@开头<br>
注释：<#-- and --><br>

## 常用指令
<p><strong>#if</strong></p>
```html
<#if animals.python.price < animals.elephant.price>
  Pythons are cheaper than elephants today.
<#elseif animals.elephant.price < animals.python.price>
  Elephants are cheaper than pythons today.
<#else>
  Elephants and pythons cost the same today.
</#if>
```

<p><strong>#list</strong></p>
```html
<table border=1>
  <#list animals as animal>
    <tr><td>${animal.name}<td>${animal.price} Euros
  </#list>
</table>
```

<p><strong>#item</strong>(只循环#item标签下的内容，如果list为空，#list下的所有内容将被略过)<br>
(从 FreeMarker 2.3.23 版本开始，之前我司的依赖还是2.3.19版本，循环都用不了items标签，简直惊呆。最近好像更新上来了。)</p>
```html
<#list misc.fruits>
  <ul>
	<#items as fruit>
	  <li>${fruit}
	</#items>
  </ul>
</#list>
```

<p><strong>#sep</strong>(分隔符指令,<#sep>, </#sep>  or <#sep>,)<br>
#list中的#else</p>
```html
Fruits: <#list misc.fruits as fruit>${fruit}<#sep>, <#else>None</#list><br>
以上可以简化为Fruits: ${fruits?join(", ", "None")}<br>
```

遍历map
```html
<#list map?keys as key><br>
<input type="text" value=${key}><br>
<input type="text" value=${map[key]}><br>
</#list><br>
</p>
```

list判空再取长度
```html
<#if switchMap??>
	switchCount = ${switchMap?size};
</#if>
```
<strong>#inlcude</strong>(可以实现在指定位置重用代码)
```html
<#include "/copyright_footer.html">
```

## 内建函数(使用?来访问)
<strong>html</strong>:给出 user 的HTML转义版本 (比如 & 会由 &amp; 来代替)
```
user?html
```
<strong>upper_case</strong>:给出 user 值的大写版本 (比如 "John Doe" 会由 "JOHN DOE" 来代替)
```
user?upper_case
```
<strong>cap_first</strong>:给出 animal.name 的首字母大写版本(比如 "mouse" 会由 "Mouse" 来替代 )
```
animal.name?cap_first
```
<strong>length</strong>:给出 user 值中字符的数量(对于 "John Doe" 来说就是8)
```
user?length
```
<strong>size</strong>:给出 animals 序列中项目的个数
```
animals?size
```
## list标签中的内建函数
<strong>index</strong>:给出了在animals中基于0开始的animal的索引值
```
animal?index
```
<strong>counter</strong>:给出了在animals中的计数个数
```
animal?counter
```
<strong>item_parity</strong>:基于当前计数的奇偶性，给出字符串 "odd" 或 "even"
```
animal?item_parity
```
## 带参数的内建函数
<strong>string</strong>:基于 animal.protected 的布尔值来返回字符串 "Y" 或 "N"。
```
animal.protected?string("Y", "N")
```
<strong>item_cycle</strong>:是之前介绍的 item_parity 更为常用的变体形式。
```
animal?item_cycle('lightRow','darkRow')
```
<strong>join</strong>:通过连接所有项，将列表转换为字符串， 在每个项之间插入参数分隔符(比如 "orange,banana")
```
fruits?join(", ")
```
<strong>starts_with</strong>:根据 user 的首字母是否是 "J" 返回布尔值true或false。
```
user?starts_with("J")
```
<font size="1" color="#FF0000"><strong>内建函数可以链式操作。比如：</strong></font>
```
user?upper_case?html
```

## 附录
“<strong>!</strong>”:插值默认值设置<br>
```
${user!"visitor"}
```
“<strong>??</strong>”:插值是否为空询问<br>
```
user??
```
通常可以配合#if访问：
```
<#if user??><h1>Welcome ${user}!</h1></#if>
```
关于多级访问的变量,只关心最后一级price是否为空，其上级为空时会抛出异常<br>
```
animals.python.price!0 
```
关注所有层级是否为空，任意一个为空则取默认值0。
```
(animals.python.price)!0 
```
