---
title: HTML-mailto用法
date: 2016-04-04 22:04:14
categories: 前端
tags: [html,前端]
---
使用
``` html
<a href=mailto:sample@163.com>send email</a>
```
或者
`<form action="mailto:sample@163.com">
    ...
</form>`
mailto后跟的是收信人
<!--more-->
可使用参数列表

| to | 	 收信人 |
|---|:------:|
|  subject | 	 收信人 |
| cc | 	 抄送 |
| bcc | 	 暗送 |
| body | 	 内容 |
参数传递方式同页面之间传递值一样，可以使用查询字符串，也可以用form
querystring方式：
``` html
<a href="mailto:sample@163.com?subject=test&cc=sample@hotmail.com&body=use mailto sample">send mail</a>
```
form方式：
``` html
<form name='sendmail' action='mailto:sample@163.com'>
    <input name='cc' type='text' value='sample@hotmail.com'>
    <input name='subject' type='text' value='test'>
    <input name='body' type='text' value='use mailto sample'>
</form>
```
两种方式同样传递所有参数。
