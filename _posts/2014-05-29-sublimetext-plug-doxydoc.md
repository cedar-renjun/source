title: 'SublimeText 插件 -- DoxyDoc'
date: 2014-05-29 08:18:37
categories:
- 教程
- SublimeText
---

## 简介

DoxyDoc是一款C++语言的Doxygen插件，有了它，你可以在SublimeText中快速插入注释，极大的提高效率

其它同类的插件有 [PhpDoc](https://github.com/SublimeText/PhpDoc) 和 [DocBlockr](https://github.com/spadgos/sublime-jsdocs)

## 安装

1.  按`Ctrl+Shift+P` 调出命令栏
2.  输入`Install Package`执行包安装命令
3.  输入`DoxyDoc`，然后点击确定，等待安装结束

## 用法

DoxyDoc会自动判断上下文环境，添加不同的注释格式，具体来说，包括两种

1.  注释处没有函数或变量，则自动创建空白注释

![]({{site.url}}/images/2014/05/29/01.gif)

2.  注释处有函数或变量，则根据函数信息自动填充对应的注释部分
    其中函数信息包括：函数名，传入参数，返回值

![]({{site.url}}/images/2014/05/29/02.gif)
![]({{site.url}}/images/2014/05/29/03.gif)
![]({{site.url}}/images/2014/05/29/04.gif)
![]({{site.url}}/images/2014/05/29/05.gif)


## 更多信息

请参考：<https://sublime.wbond.net/packages/DoxyDoc>