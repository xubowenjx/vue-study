# 自定义报表实现思路
 
>通过前后端分离-前端展示和数据完全分开。
使用Vue作为前端框架,将常用HTML组件封装成模块,将复杂的前台界面以简单的形式模块化,使用时按需加载既可以。
做到一次封装，重复使用。


## 0. 为什么要这么做?
>与正常的开发不同之处在于:<br/>
1.我们不知道布局,甚至不知道你需要展现什么。<br/>
2.我们不知道数据。即使有SQL能给我们什么,只能给我们查询结果而已，但是具体的展现是不能决定的。<br/>
3.为什么要前后端分离。jsp动态界面技术需要走容器解析java代码并生成html文档，但是基于1、2了解到我们什么都不知道。
<br/>4.这么做的意义。我们需要做一个可维护、高可用的东西，并且你所看到的东西并不是因为代码就是这么写的。
而是因为数据驱动着你眼前的一切。只要数据在,界面就在。
<br/>


## 1.前台到后台还是后台到前台?
>自定义报表之所以称之为自定义,就是在上面都不知道的前提下,通过一系列的操作
达到报表的功能。关键在于2点：1前台展示,2数据来源。

## 2.基于元数据的数据驱动形式

>设计元数据 决定前端展示和数据来源。<br/>
1.我们认为表字段的可以作为前端组件展示,比如一个No我们可以认为是一个input,
一个p_code我们认为是一个select。但是这种方式有一个缺点,所有的东西都是基于元数据,
一变则万变。一个数据无法同时作为多个类型展示。<br>
2.元数据构造查询。报表数据由查询SQL决定，而一个SQL又可以拆分成三部分：
1.select,2.from,3,where. select 部分由数据展示的表格决定,表格的表头即select需要的字段。
from部分则是数据来源的数据库表.where部分则是查询表单决定。

## 3.实现报表

>难点在于实用性。为了满足实际需要，组件会不断的扩大、丰富,数据也变得越加复杂。
纵观现阶段完成的功能，觉得部分都是在数据处理上花时间。
而整个流程就是``一来一回``,首先你得先实现`展示`和`功能`,接下来就是考虑复用性，
如何把你设计的报表转化成一堆数据，然后由这堆数据再展现成原来的界面。
其实,``组件只是个容器,里面的东西可以不需要直接从别的地方拿,也可以自己去生产.``


