---
layout: post
title: "在Doxygen中使用Markdown"
date: 2014-03-27 09:34:57 +0800
comments: true
categories: [教程，Doxygen，Markdown]
published: true
---

开源爱好者和官方API库经常会使用Doxygen来为代码添加注释，只需要维护一份代码文件，便可以生成代码和文档功能，从而避免文档和代码严重不一致的情况

但Doxygen的缺点也非常明显，注释规则复杂，直接看不容易看懂，不适合生成专业文档

很多时候，我们既希望生成漂亮的文档，又想在文档内不含有复杂的语法规则，普通人也能直接看懂原文档，有没有这种东西呢？

有！ Markdown便是这样一种文档书写语言，用户只需要关心文档内容，不需要关心具体表现形式，Markdown编辑器会帮你做这些工作

Markdown官方解释如下：

> **宗旨**
> 
> Markdown 的目标是实现「易读易写」。
>
> 可读性，无论如何，都是最重要的。一份使用Markdown格式撰写的文件应该可以直接以纯文本发布，
> 并且看起来不会像是由许多标签或是格式指令所构成。
>
> Markdown 语法受到一些既有 text-to-HTML 格式的影响，包括 Setext、atx、Textile、reStructuredText、
> Grutatext和EtText，而最大灵感来源其实是纯文本电子邮件的格式。
>
> 总之， Markdown 的语法全由一些符号所组成，这些符号经过精挑细选，其作用一目了然。
> 比如：在文字两旁加上星号，看起来就像*强调*。Markdown 的列表看起来，嗯，就是列表。
> Markdown 的区块引用看起来就真的像是引用一段文字，就像你曾在电子邮件中见过的那样

貌似很不错的样子，是吧，事实上，github上很多文档都是按照Markdown语法来写的。

如果您是第一次听说Markdown，这里有一个简短的中文入门教程

<http://wowubuntu.com/markdown/basic.html>

既然Markdown这么好用，如果Doxygen中也能使用Markdown就更好了，既能方便的为代码注释，也能脱离代码，编写大型专业文档，即使以后不用Doxygen输出文档，我们也可以采用其他的markdown编辑器来输出文档


ok，下面让我们来看看如何在Doxygen中使用Markdown


**注：**在继续阅读之前，请确保您熟悉Doxygen的基本操作和常用语法；如果您没接触过Doxygen，请先阅读《Doxygen 10分钟入门教程》

<!-- more -->

## 第一次尝试

创建一个空文件夹，这里假设为：`Markdown`，然后新建一个文件，名为readme.md，内容如下

    Description {#mainpage}
    =======================

    ## 介绍

    这是我们编写的第一个Markdown文件

    ## 下一步要做什么？

    接下来，我们详细学习Markdown语法以及介绍Doxygen中的注意事项

然后用默认Doxygen配置文档，在当前目录下编译，打开对应的html网页文件，如下图所示


![Markdown_Demo]({{site.url}}/images/2014/03/27/Markdown_Demo.jpg)


这便是我们在doxygen下生成的第一个markdown文档

    1：新建一个*.md文件
    2：在这里编写符合Markdown语法的文字
    3：编译输出HTML

很简单吧

**注：**需要保证readmd.md文件编码格式为`UTF-8`

## Markdown标准语法

我们已经知道怎么在Doxygen下使用Markdown了，接下来，让我们详细的学习一下Markdown的基本语法规则

### 1. 标题

【语法规则】

Markdown 支持两种标题的语法，类Setext和类atx形式。

类 Setext 形式是用底线的形式，利用 `=` （最高阶标题）和 `-` （次高阶标题），例如：

	示例1

    This is an H1
    =============

    This is an H2
    -------------

任何数量的 `=` 和 `-` 都可以有效果

类 Atx 形式则是在行首插入 1 到 6 个 `#` ，对应到标题 1 到 6 阶，例如：

	示例2

    # 这是 H1

    ## 这是 H2

    ###### 这是 H6

你可以选择性地「闭合」类 atx 样式的标题，这纯粹只是美观用的，若是觉得这样看起来比较舒适，你就可以在行尾加上 `#`，而行尾的 `#` 数量也不用和开头一样（行首的井字符数量决定标题的阶数）：

	示例3

    # 这是 H1 #

    ## 这是 H2 ##

    ### 这是 H3 ######

【效果展示】

**示例1**

This is an H1
=============

This is an H2
-------------


**示例2**

# 这是 H1

## 这是 H2

###### 这是 H6


**示例3**

# 这是 H1 #

## 这是 H2 ##

### 这是 H3 ######


【注意事项】

**1:** 对于类Setext形式的标题，对于`=`或者`-`的数量，标准语法要求至少 <font color="red"> 一个 </font>，而Doxygen要求至少<font color="red">两个</font>

**2:** 对于一级标题，Doxygen有特殊要求，详情参见[Markdown拓展语法--标题章节]

### 2. 段落和换行

【语法规则】

一个 Markdown 段落是由一个或多个连续的文本行组成，它的前后要有一个以上的空行

**注：**这里的空行是仅由“空格”，“TAB制表符”，“回车符”三者组成的行

换行的方式有两种：

1）在段落任意处插入`<br/>`来强制换行

2）在行末尾加**两个以上**空格

【效果展示】

**原Markdown文本**

	这是一个段落

	这也是一个段落

	这是一个段落
	这是段落中的某句话

	这是通过加空格来换行的段落  
	这是通过加空格来换行的段落  
	这是通过加空格来换行的段落  
	这是通过加空格来换行的段落  

	这是没有换行的段落,
	这是没有换行的段落,
	这是没有换行的段落,
	这是没有换行的段落,
	这是没有换行的段落

<br/>**输出HTML效果**<br/>

这是一个段落

这也是一个段落

这是一个段落
这是段落中的某句话

这是通过加空格来换行的段落  
这是通过加空格来换行的段落  
这是通过加空格来换行的段落  
这是通过加空格来换行的段落  

这是没有换行的段落,
这是没有换行的段落,
这是没有换行的段落,
这是没有换行的段落,
这是没有换行的段落

【注意事项】

**1：**普通段落不该用空格或制表符来缩进，否则会被编译器当做“预格式化文本”来处理

**2：**Doxygen不支持**在行尾加空格**这种方式来换行，如果您必须在段落中换行，
请采用插入`<br/>`的方式来进行

### 3. 引用

【语法规则】

Markdown 标记区块引用是使用类似 email 中用 `>` 的引用方式。如果你还熟悉在 email 信件中的引言部分，你就知道怎么在Markdown文件中建立一个区块引用，那会看起来像是你自己先断好行，然后在每行的最前面加上 `>` ：

	示例1
	> A Thai satellite has detected some 300 objects in an area of 
	> the southern Indian Ocean being searched for missing Malaysia 
	> Airlines flight MH370.
	> 
	> The image was taken by the Thaichote satellite on 24 March, 
	> a day after images from a French satellite purported to show 
	> 122 floating objects.
	> 
	> Flight MH370 disappeared on 8 March with 239 people on board. 
	> No debris has been recovered from the ocean so far.

Markdown 也允许你偷懒只在整个段落的第一行最前面加上 `>` ：

	示例2
	> A Thai satellite has detected some 300 objects in an area of 
	the southern Indian Ocean being searched for missing Malaysia 
	Airlines flight MH370.
	 
	> The image was taken by the Thaichote satellite on 24 March, 
	a day after images from a French satellite purported to show 
	122 floating objects.

	> Flight MH370 disappeared on 8 March with 239 people on board. 
	No debris has been recovered from the ocean so far.

区块引用可以嵌套（例如：引用内的引用），只要根据层次加上不同数量的 `>` ：

	示例3
    > This is the first level of quoting.
    >
    > > This is nested blockquote.
    >
    > Back to the first level.

引用的区块内也可以使用其他的 Markdown 语法，包括标题、列表、代码区块等：

	示例4
	> ## This is a header
	> 
	> 1.   This is first item
	> 2.   This is second item
	> 
	> Here, Show code snippet for you:
	>     return shell_exec("echo $input | $markdown_script");

【效果展示】

<br/>
**示例1**

> A Thai satellite has detected some 300 objects in an area of 
> the southern Indian Ocean being searched for missing Malaysia 
> Airlines flight MH370.
> 
> The image was taken by the Thaichote satellite on 24 March, 
> a day after images from a French satellite purported to show 
> 122 floating objects.
> 
> Flight MH370 disappeared on 8 March with 239 people on board. 
> No debris has been recovered from the ocean so far.


<br/>
**示例2**

> A Thai satellite has detected some 300 objects in an area of 
the southern Indian Ocean being searched for missing Malaysia 
Airlines flight MH370.
 
> The image was taken by the Thaichote satellite on 24 March, 
a day after images from a French satellite purported to show 
122 floating objects.

> Flight MH370 disappeared on 8 March with 239 people on board. 
No debris has been recovered from the ocean so far.


<br/>
**示例3**

> This is the first level of quoting.
>
> > This is nested blockquote.
>
> Back to the first level.


<br/>
**示例4**

> ## This is a header
> 
> 1.   This is first item
> 2.   This is second item
> 
> Here, Show code snippet for you:
>
>     return shell_exec("echo $input | $markdown_script");

【注意事项】

**1：**Doxygen不支持省略`>`的形式（如示例2），如果您需要确保引用块的每行前都有`>`

**2：**在Doxygen环境下，如果需要在引用块中插入其他Markdown语法块，请确保每个块之间
至少保持一个空行，下面代码，在Doxygen中无法生效：

	> Here, Show code snippet for you:
	>     return shell_exec("echo $input | $markdown_script");

因为中间少了一个空行

### 4. 列表

【语法规则】

Markdown 支持有序列表和无序列表

无序列表使用星号（*）、加号（+）或是减号（-）作为列表标记：

    示例1

    *   Red
    *   Green
    *   Blue
    或者
    +   Red
    +   Green
    +   Blue    
    或者
    -   Red
    -   Green
    -   Blue

有序列表则使用数字接着一个英文句点：

    示例2

    1.  Bird
    2.  McHale
    3.  Parish

很重要的一点是，你在列表标记上使用的数字并不会影响输出的 HTML 结果，上面的列表所产生的 HTML 标记为：

    <ol>
    <li>Bird</li>
    <li>McHale</li>
    <li>Parish</li>
    </ol>

如果你的列表标记写成：

    示例3

    1.  Bird
    1.  McHale
    1.  Parish

或甚至是：

    示例4

    3. Bird
    1. McHale
    8. Parish

你都会得到完全相同的HTML输出。重点在于，你可以让Markdown文件的列表数字和输出的结果相同，或是你懒一点，你可以完全不用在意数字的正确性

如果你使用懒惰的写法，建议第一个项目最好还是从 1. 开始，因为 Markdown 未来可能会支持有序列表的 start 属性

列表项目标记通常是放在最左边，但是其实也可以缩进，最多3个空格，项目标记后面则一定要接着至少一个空格或制表符

要让列表看起来更漂亮，你可以把内容用固定的缩进整理好：

    示例5

    *   Lorem ipsum dolor sit amet, consectetuer adipiscing elit.
        Aliquam hendrerit mi posuere lectus. Vestibulum enim wisi,
        viverra nec, fringilla in, laoreet vitae, risus.
    *   Donec sit amet nisl. Aliquam semper ipsum sit amet velit.
        Suspendisse id sem consectetuer libero luctus adipiscing.

但是如果你懒，那也行：

    示例6

    *   Lorem ipsum dolor sit amet, consectetuer adipiscing elit.
    Aliquam hendrerit mi posuere lectus. Vestibulum enim wisi,
    viverra nec, fringilla in, laoreet vitae, risus.
    *   Donec sit amet nisl. Aliquam semper ipsum sit amet velit.
    Suspendisse id sem consectetuer libero luctus adipiscing.

如果列表项目间用空行分开，在输出 HTML 时 Markdown 就会将项目内容用 `<p>` 
标签包起来，举例来说：

    示例7

    *   Bird
    *   Magic

会被转换为：

    <ul>
    <li>Bird</li>
    <li>Magic</li>
    </ul>

但是这个：

    示例8

    *   Bird

    *   Magic

会被转换为：

    <ul>
    <li><p>Bird</p></li>
    <li><p>Magic</p></li>
    </ul>

列表项目可以包含多个段落，每个项目下的段落都必须缩进 4 个空格或是 1 个制表符：

    示例9

    1.  This is a list item with two paragraphs. Lorem ipsum dolor
        sit amet, consectetuer adipiscing elit. Aliquam hendrerit
        mi posuere lectus.

        Vestibulum enim wisi, viverra nec, fringilla in, laoreet
        vitae, risus. Donec sit amet nisl. Aliquam semper ipsum
        sit amet velit.

    2.  Suspendisse id sem consectetuer libero luctus adipiscing.

如果你每行都有缩进，看起来会看好很多，当然，再次地，如果你很懒惰，Markdown 也允许：

    示例10

    *   This is a list item with two paragraphs.

        This is the second paragraph in the list item. You're
    only required to indent the first line. Lorem ipsum dolor
    sit amet, consectetuer adipiscing elit.

    *   Another item in the same list.

如果要在列表项目内放进引用，那 `>` 就需要缩进：

    示例11

    *   A list item with a blockquote:

        > This is a blockquote
        > inside a list item.

如果要放代码区块的话，该区块就需要缩进*两次*，也就是 8 个空格或是 2 个制表符：

    示例12

    *   一列表项包含一个列表区块：

            extern int main(void);

当然，项目列表很可能会不小心产生，像是下面这样的写法：

    1986. What a great season.

换句话说，也就是在行首出现*数字-句点-空白*，要避免这样的状况，你可以在句点前面加上反斜杠。

    1986\. What a great season.

【效果展示】

<br/>
**示例1：**

*   Red
*   Green
*   Blue


<br/>
**示例2、3、4：**

1.  Bird
2.  McHale
3.  Parish


<br/>
**示例5、6：**

*   Lorem ipsum dolor sit amet, consectetuer adipiscing elit.
    Aliquam hendrerit mi posuere lectus. Vestibulum enim wisi,
    viverra nec, fringilla in, laoreet vitae, risus.
*   Donec sit amet nisl. Aliquam semper ipsum sit amet velit.
    Suspendisse id sem consectetuer libero luctus adipiscing.


<br/>
**示例7：**

*   Bird
*   Magic


<br/>
**示例8：**

*   Bird

*   Magic


<br/>
**示例9：**

1.  This is a list item with two paragraphs. Lorem ipsum dolor
    sit amet, consectetuer adipiscing elit. Aliquam hendrerit
    mi posuere lectus.

    Vestibulum enim wisi, viverra nec, fringilla in, laoreet
    vitae, risus. Donec sit amet nisl. Aliquam semper ipsum
    sit amet velit.

2.  Suspendisse id sem consectetuer libero luctus adipiscing.


<br/>
**示例11：**

*   A list item with a blockquote:

    > This is a blockquote
    > inside a list item.


<br/>
**示例12：**
    
*   一列表项包含一个列表区块：

        extern int main(void);


【注意事项】

Doxygen对于列表的处理比较特殊，具体如下

*   会将用空行隔开的两个列表项当成同一个列表项来处理
    【占位符】举例
*   对于有序列表，严格按照升序来处理，一旦发现相等或者降序排列，则认为下一个为新的列表开始点
    【占位符】举例
*   有序列表里面的实际序号，并不影响HTML输出结果的显示
    【占位符】举例

### 5. 代码区块

【语法规则】

和程序相关的写作或是标签语言原始码通常会有已经排版好的代码区块，通常这些区块我们并不希望它以一般段落文件的方式去排版，而是照原来的样子显示，Markdown 会用 `<pre>` 和 `<code>` 标签来把代码区块包起来。

要在 Markdown 中建立代码区块很简单，只要简单地缩进 4 个空格或是 1 个制表符就可以，例如，下面的输入：

    示例1
    这是一个普通段落：

        这是一个代码区块。

Markdown 会转换成：

    <p>这是一个普通段落：</p>

    <pre><code>这是一个代码区块。
    </code></pre>

这个每行一阶的缩进（4 个空格或是 1 个制表符），都会被移除，例如：

    示例2
    Here is an example of AppleScript:

        tell application "Foo"
            beep
        end tell

会被转换为：

    <p>Here is an example of AppleScript:</p>

    <pre><code>tell application "Foo"
        beep
    end tell
    </code></pre>

一个代码区块会一直持续到没有缩进的那一行（或是文件结尾）。

在代码区块里面， `&` 、 `<` 和 `>` 会自动转成 HTML 实体，这样的方式让你非常容易使用 Markdown 插入范例用的 HTML 原始码，只需要复制贴上，再加上缩进就可以了，剩下的 Markdown 都会帮你处理，例如：

        <div class="footer">
            &copy; 2004 Foo Corporation
        </div>

会被转换为：

    <pre><code>&lt;div class="footer"&gt;
        &amp;copy; 2004 Foo Corporation
    &lt;/div&gt;
    </code></pre>

代码区块中，一般的 Markdown 语法不会被转换，像是星号便只是星号，这表示你可以很容易地以 Markdown 语法撰写 Markdown 语法相关的文件。

【效果展示】

参见语法规则中的：**示例1**，**示例2** 部分

【注意事项】


**“要在 Markdown 中建立代码区块很简单，只要简单地缩进 4 个空格或是 1 个制表符”**

这里有两点需要注意：

**1：** 使用TAB需谨慎

Doxygen和某些Markdown编辑器会将制表符替换成一定数量的空格，然后再进行处理，这种情况下，
就等同于文档中仅有空格来表示缩进。

此时，“制表符等于几个空格（TAB = N Space）”这个问题，变得尤为关键，当N等于4时，一切都很正常，符合预期结果；
当N大于4时，编辑器会首先减去4个空格，然后将多余的空格当成代码的一部分来解释；当N小于4时，
编辑器将首先去除这多余的N歌空格，然后把剩下的部分作为普通文本段落来处理

**注：**您可以通过修改Doxygen工程配置文件中的

    # The TAB_SIZE tag can be used to set the number of spaces in a tab. Doxygen
    # uses this value to replace tabs by spaces in code fragments.
    # Minimum value: 1, maximum value: 16, default value: 4.

    TAB_SIZE               = 4

来设置指标符和空格的置换关系


**建议：**文档里面不要使用TAB，在您的文本编辑器里面将TAB设置为4个空格，这样可以避免很多潜在的问题


**2：**4个空格偏移量是相对于谁来说的？

标准Markdown语法中，仅说明了代码块前需要4个空格偏移量，但没说这个偏移量是相对于谁来计算的，默认情况下，是相对于文档最左边第一列，这里把代码块相对于最左边的偏移量（以空格为单位）称之为**绝对偏移**

一般情况下，绝对偏移的阈值为4，只要某个段落缩进不超过4，则把它当做普通段落来处理。如果检测到绝对偏移超过8，则首先判断它是不是在列表中，如果是，则将该部分做为列表代码块来处理；如果不是，则将该部分作为普通代码块来处理

这里，我们可以看到，绝对定位原则在标准Markdown编辑器中扮演着非常重要的角色

Doxygen中也是这样吗？不是的，因为Doxygen不仅仅要处理纯Markdown文本，还要处理代码注释中插入的Markdown文本，而注释文本可以有任意缩进量，如果不做处理，就会导致一些错误。因此Doxygen采用**相对偏移**的方式来代替标准Markdown编辑器的绝对偏移方式，即：

**本段落偏移量是相对于上一个段落来计算的**

**注：**在列表中的相对便宜了计算，不包括列表标记符号

一般情况下，Doxygen的这种处理方式，对正常编写的Markdown文本，不会造成任何错误，除非你采用下面的形式

    text     相对于上个段落，偏移0个空格；相对于行首，绝对偏移0个空格

     text    相对于上个段落，偏移1个空格；相对于行首，绝对偏移1个空格

      text   相对于上个段落，偏移1个空格；相对于行首，绝对偏移2个空格

        code 相对于上个段落，偏移2个空格；相对于行首，绝对偏移4个空格

这种情况下，markdown编辑器会将`code`那行当做代码行，但Doxygen不会，因为相对偏移只有2个空格

### 6. 分隔线

【语法规则】

你可以在一行中用**三个以上**的星号（*）、减号（-）、底线（_）来建立一个分隔线，行内不能有其他东西

    示例1

    ***
    ---
    ___


同时星号或是减号中间允许插入空格，像下面这样

    示例2

*  *  *
-  -  -    

<br/>
【效果展示】

**示例1：**下面是3个分割线

***
---
___


<br/>
**示例2：**下面是2个分割线

*  *  *
-  -  -

<br/>
【注意事项】

**1：**标准Markdown编辑器支持上面所有规范，但Doxygen要求在分割线单独作为一行，且前后保留空行
，其它编辑器也会做这个要求。

所以建议：在使用分割线的时候，将分隔线单独作为一行，且**前后保留至少一个空行**

如下所示

    这里是段落

    ***

    这里也是段落，接下来要插入三个分割线

    ---

    ***

    ___


而不要像这样写（特别注意最后三个分隔符）：

    这里是段落

    ***

    这里也是段落，接下来要插入三个分割线

    ---
    ***
    ___

**2：**对于Doxygen来说，分割线仅在Markdown文件中生效，代码注释中无法生效

比如下面这样：

    /** A list:
     *  * item1
     *  *******
     *  * item2
     */

`item1`和`item2`之间不会插入分割线

### 7. 链接

【语法规则】

Markdown 支持两种形式的链接语法： *行内式*和*参考式*两种形式。

不管是哪一种，链接文字都是用 [方括号] 来标记。

要建立一个*行内式*的链接，只要在方块括号后面紧接着圆括号并插入网址链接即可，如果你还想要加上链接的 title 文字，只要在网址后面，用双引号把 title 文字包起来即可，例如：

    示例1

    This is [an example](http://example.com/ "Title") inline link.

    [This link](http://example.net/) has no title attribute.

会产生：

    <p>This is <a href="http://example.com/" title="Title">
    an example</a> inline link.</p>

    <p><a href="http://example.net/">This link</a> has no
    title attribute.</p>

如果你是要链接到同样主机的资源，你可以使用相对路径：

    See my [About](/about/) page for details.   

*参考式*的链接是在链接文字的括号后面再接上另一个方括号，而在第二个方括号里面要填入用以辨识链接的标记：
    
    示例2

    This is [an example][id] reference-style link.

你也可以选择性地在两个方括号中间加上一个空格：

    This is [an example] [id] reference-style link.

接着，在文件的任意处，你可以把这个标记的链接内容定义出来：

    [id]: http://example.com/  "Optional Title Here"

链接内容定义的形式为：

*   方括号（前面可以选择性地加上至多三个空格来缩进），里面输入链接文字
*   接着一个冒号
*   接着一个以上的空格或制表符
*   接着链接的网址
*   选择性地接着 title 内容，可以用单引号、双引号或是括弧包着

下面这三种链接的定义都是相同：

    [foo]: http://example.com/  "Optional Title Here"
    [foo]: http://example.com/  'Optional Title Here'
    [foo]: http://example.com/  (Optional Title Here)

**请注意：**有一个已知的问题是 Markdown.pl 1.0.1 会忽略单引号包起来的链接 title。

链接网址也可以用方括号包起来：

    [id]: <http://example.com/>  "Optional Title Here"

你也可以把 title 属性放到下一行，也可以加一些缩进，若网址太长的话，这样会比较好看：

    [id]: http://example.com/longish/path/to/resource/here
        "Optional Title Here"

网址定义只有在产生链接的时候用到，并不会直接出现在文件之中。

链接辨别标签可以有字母、数字、空白和标点符号，但是并*不*区分大小写，因此下面两个链接是一样的：

    [link text][a]
    [link text][A]

*隐式链接标记*功能让你可以省略指定链接标记，这种情形下，链接标记会视为等同于链接文字，要用隐式链接标记只要在链接文字后面加上一个空的方括号，如果你要让 "Google" 链接到 google.com，你可以简化成：

    [Google][]

然后定义链接内容：

    [Google]: http://google.com/

由于链接文字可能包含空白，所以这种简化型的标记内也许包含多个单词：

    Visit [Daring Fireball][] for more information.

然后接着定义链接：

    [Daring Fireball]: http://daringfireball.net/

链接的定义可以放在文件中的任何一个地方，我比较偏好直接放在链接出现段落的后面，你也可以把它放在文件最后面，就像是注解一样。

下面是一个参考式链接的范例：

    I get 10 times more traffic from [Google] [1] than from
    [Yahoo] [2] or [MSN] [3].

      [1]: http://google.com/        "Google"
      [2]: http://search.yahoo.com/  "Yahoo Search"
      [3]: http://search.msn.com/    "MSN Search"

如果改成用链接名称的方式写：

    I get 10 times more traffic from [Google][] than from
    [Yahoo][] or [MSN][].

      [google]: http://google.com/        "Google"
      [yahoo]:  http://search.yahoo.com/  "Yahoo Search"
      [msn]:    http://search.msn.com/    "MSN Search"

上面两种写法都会产生下面的 HTML。

    <p>I get 10 times more traffic from <a href="http://google.com/"
    title="Google">Google</a> than from
    <a href="http://search.yahoo.com/" title="Yahoo Search">Yahoo</a>
    or <a href="http://search.msn.com/" title="MSN Search">MSN</a>.</p>

下面是用行内式写的同样一段内容的 Markdown 文件，提供作为比较之用：

    I get 10 times more traffic from [Google](http://google.com/ "Google")
    than from [Yahoo](http://search.yahoo.com/ "Yahoo Search") or
    [MSN](http://search.msn.com/ "MSN Search").

参考式的链接其实重点不在于它比较好写，而是它比较好读，比较一下上面的范例，使用参考式的文章本身只有 81 个字符，但是用行内形式的却会增加到 176 个字元，如果是用纯 HTML 格式来写，会有 234 个字元，在 HTML 格式中，标签比文本还要多。

使用 Markdown 的参考式链接，可以让文件更像是浏览器最后产生的结果，让你可以把一些标记相关的元数据移到段落文字之外，你就可以增加链接而不让文章的阅读感觉被打断。

【效果展示】

<br/>
**示例1**
    
This is [an example](http://example.com/ "Title") inline link.

[This link](http://example.net/) has no title attribute.

<br/>
**示例2**

This is [an example][id] reference-style link.

[id]: http://example.com/  "Optional Title Here"

【注意事项】

**1：** 参考式链接，可以用来创建文档内链接，如下所示

    *   [概述](#overview)
    *   [安装](#install)

    <h2 id="overview">概述</h2>
    <h2 id="philosophy">安装</h2>

**2：** 在使用链接的时候，网址前必须要有`http://`头部，否则会跳转失败

**3：** 某些Markdown编译器不支持参考式链接中的单引号标题，建议采用标准双引号的形式

### 8. 强调

【语法规则】

Markdown 使用星号（`*`）和底线（`_`）作为标记强调字词的符号，被 `*` 或 `_` 包围的字词会被转成用 `<em>` 标签包围，用两个 `*` 或 `_` 包起来的话，则会被转成 `<strong>`，例如：

    示例1

    *single asterisks*

    _single underscores_

    **double asterisks**

    __double underscores__

会转成：

    <em>single asterisks</em>

    <em>single underscores</em>

    <strong>double asterisks</strong>

    <strong>double underscores</strong>

你可以随便用你喜欢的样式，唯一的限制是，你用什么符号开启标签，就要用什么符号结束。

强调也可以直接插在文字中间：

    示例2

    un*frigging*believable

但是**如果你的 `*` 和 `_` 两边都有空白的话，它们就只会被当成普通的符号**，如下所示

    示例3

    This is a single asterisk * .

如果要在文字前后直接插入普通的星号或底线，你可以用反斜线：

    示例4

    \*this text is surrounded by literal asterisks\*

<br/>
【效果展示】

**示例1**

*single asterisks*

_single underscores_

**double asterisks**

__double underscores__


<br/>
**示例2**

un*frigging*believable


<br/>
**示例3**

This is a single asterisk * .


<br/>
**示例4**

\*this text is surrounded by literal asterisks\*


【注意事项】

**1：**某些编辑器可能不支持**示例2**中的Markdown语法

    示例2

    un*frigging*believable    

如果需要用`*`来强调，请确保"开始标签前"和"关闭标签后"各含一个空格，如下所示

    示例2修改版

    un *frigging* believable

    un *frigging believable* Flag

    un **frigging** believable

    un **frigging believable** Flag

如果必须要强调单词中某个词，请直接采用`<em>`或`<strong>`，如下所示

    un<em>frigging</em>believable 

    un<strong>frigging</strong>believable 

**2：**Doxygen无法用`*`形式来强调中文字符，请直接采用`<em>`或`<strong>`来强调

**3：**某些Markdown编辑器允许在强调文字中断行，如下所示

    部分编辑器支持换行

    **Line1
    Line2
    Line3**

但很多编译器不支持这种格式，同时，几乎所有的编辑器都不支持断行，如下所示

    不能用*来强调多个段落文字

    **Line1

    Line2

    Line3**

**4：**在Doxygen中，标题默认是强调的，请不要额外添加`*`来表示强调



**5：**Doxygen只有在满足下面的条件下，才认为是强调

开始条件：

后：字母或者数字  
前：空格，新行，或者下面任一个字符`<` `{` `(` `[` `,` `:` `;`

结束条件：

后：不是字母或者数字  
前：不是空格，新航，或者下面任一个字符`(` `{` `[` `<` `=` `+` `-` `\` `@`

**6：**在Doxygen中，`*`或`_`作用范围限制在段落内

### 9. 代码

【语法规则】

如果要标记一小段行内代码，你可以用反引号把它包起来（`）

**注：**反引号指位于键盘数字键1的左方，Tab键上方的那个键，千万别当做单引号了！

例如：

    示例1

    Use the `printf()` function.

会生成下面的HTML代码：

    <p>Use the <code>printf()</code> function.</p>

如果要在代码区段内插入反引号，你可以用多个反引号来开启和结束代码区段：

    示例2

    ``There is a literal backtick (`) here.``

这段语法会产生：

    <p><code>There is a literal backtick (`) here.</code></p>

代码区段的起始和结束端都可以放入一个空白，起始端后面一个，结束端前面一个，这样你就可以在区段的一开始就插入反引号：

    示例3

    A single backtick in a code span: `` ` ``

    A backtick-delimited string in a code span: `` `foo` ``

会产生：

    <p>A single backtick in a code span: <code>`</code></p>

    <p>A backtick-delimited string in a code span: <code>`foo`</code></p>

在代码区段内，& 和方括号都会被自动地转成 HTML 实体，这使得插入 HTML 原始码变得很容易，Markdown 会把下面这段：

    示例4

    Please don't use any `<pre>` tags.

转换为

    <p>Please don't use any <code>&lt;pre&gt;</code> tags.</p>


【效果展示】


<br/>
**示例1**

Use the `printf()` function.


<br/>
**示例2**

``There is a literal backtick (`) here.``


<br/>
**示例3**

A single backtick in a code span: `` ` ``

A backtick-delimited string in a code span: `` `foo` ``


<br/>
**示例4**

Please don't use any `<pre>` tags.

【注意事项】

**1：**本节所描述的方法适合插入少量代码语句

**2：**各个编辑器提供额外的处理机制，来处理在Markdown插入大量代码的情况；
常见的方式有

A: 插入3个反引号

    ```

    Here is your code

    ```

**注：**git的GFM采用这种方式，且可以在`` ``` ``后增加语言指示符来提供代码高亮功能


B：插入3个以上的波浪号

    ~~~

    Here is your code

    ~~~

**3：**Doxygen对代码块有特殊处理命令，详细情况，请参考**Markdown拓展语法**章节

**4：**Doxygen无法处理代码中含有单引号的情况，如下所示

    A `cool' word in a `nice' sentence.

这种情况下，请用代码块

### 10. 图片

【语法规则】

Markdown 使用一种和链接很相似的语法来标记图片，同样也允许两种样式： *行内式*和*参考式*。

简单的来说，就是在普通链接前面加一个`!`号，就是图片链接了

行内式的图片语法看起来像是：

    ![Alt text](/path/to/img.jpg)

    ![Alt text](/path/to/img.jpg "Optional title")

详细叙述如下：

*   一个惊叹号 `!`
*   接着一个方括号，里面放上图片的替代文字
*   接着一个普通括号，里面放上图片的网址，最后还可以用引号包住并加上
    选择性的 'title' 文字

**注：**路径可以是相对路径，也可以是网络绝对路径

参考式的图片语法则长得像这样：

    ![Alt text][id]

「id」是图片参考的名称，图片参考的定义方式则和连结参考一样：

    [id]: url/to/image  "Optional title attribute"


【效果展示】

**示例1：**网络图片

代码

    ![CooCox Logo](http://coocox.com/images/CooCox.gif "CooCox Logo")

效果

![CooCox Logo](http://coocox.com/images/CooCox.gif "CooCox Logo")


<br/>
**示例2：**本地图片

代码

    ![Beautiful Girl](/images/2014/03/27/LocalPic.jpg "Beautiful Girl")

效果

![Beautiful Girl](/images/2014/03/27/LocalPic.jpg "Beautiful Girl")


【注意事项】

**1：**Markdown仅提供图片链接机制，不负责具体图片文件管理。在Doxygen环境下，如果文档中链接
了本地图片资源，您必须手工将需要的图片资源复制到HTML输出文件夹中，这样才能正确显示出图片

**2：**
建议不要在链接符号，标题和链接地址保持在一个行内，否则导致Markdown解析器无法解析

### 11. 自动链接

【语法规则】

用`<`和`>`将链接地址或者邮电地址包括起来，Markdown编辑器就会为其自动创建链接

下面代码

    示例1

    <http://www.google.com.cn>

    <xxx@gmail.com>

会产生对应的HTML代码

    <p><a href="http://www.google.com">http://www.google.com</a></p>

    <p><a href="mailto:xxx@gmail.com">xxx@gmail.com</a></p>


【效果展示】

<br/>
**示例1**

<http://www.google.com.cn>

<xxx@gmail.com>

【注意事项】

**1：**网址必须是完整，有效网址，包含`http://`或者`https://`，下面的代码无法生成正确链接

    <www.google.com.cn>
    <google.com.cn>

### 12. 兼容HTML

【语法规则】

如果您熟悉HTML语法，则可以直接在文档里面用 HTML 撰写，不需要额外标注这是 HTML 或是 Markdown；只要直接加标签就可以了

要制约的只有一些 HTML 区块元素――比如 `<div>`、`<table>`、`<pre>`、`<p>` 等标签，必须在前后加上空行与其它内容区隔开，还要求它们的开始标签与结尾标签不能用制表符或空格来缩进。Markdown 的生成器有足够智能，不会在 HTML 区块标签外加上不必要的 `<p>` 标签

例子如下，在 Markdown 文件里加上一段 HTML 表格：

    示例1：在Markdown中插入HTML表格

    这是一个普通段落

    <table>
        <tr>
            <td>1</td>
            <td>2</td>
            <td>3</td>
        </tr>
        <tr>
            <td>4</td>
            <td>5</td>
            <td>6</td>
        </tr>
        <tr>
            <td>7</td>
            <td>8</td>
            <td>9</td>
        </tr>
    </table>

    这是另一个普通段落

请注意，在 HTML 区块标签间的 Markdown 格式语法将不会被处理。比如，你在 HTML 区块内使用 Markdown 样式的`*强调*`会没有效果

HTML 的区段（行内）标签如 `<span>`、`<cite>`、`<del>` 可以在 Markdown 的段落、列表或是标题里随意使用。依照个人习惯，甚至可以不用 Markdown 格式，而直接采用 HTML 标签来格式化。举例说明：如果比较喜欢 HTML 的 `<a>` 或 `<img>` 标签，可以直接使用这些标签，而不用 Markdown 提供的链接或是图像标签语法。

    示例2：通过HTML强调某个单词，为单词加颜色

    这是<strong>粗体</strong>，这是<font color="red">红色</font>

和处在 HTML 区块标签间不同，Markdown 语法在 HTML 区段标签间是有效的


【效果展示】

<br/>
**示例1：**在Markdown中插入HTML表格

这是一个普通段落

<table>
    <tr>
        <td>1</td>
        <td>2</td>
        <td>3</td>
    </tr>
    <tr>
        <td>4</td>
        <td>5</td>
        <td>6</td>
    </tr>
    <tr>
        <td>7</td>
        <td>8</td>
        <td>9</td>
    </tr>
</table>

这是另一个普通段落


<br/>
**示例2：**通过HTML强调某个单词，为单词加颜色

这是<strong>粗体</strong>，这是<font color="red">红色</font>


<br/>
**示例3：**这是一个按钮

<button type="input" title="Test Button">Button</button>


【注意事项】

**1：**
Doxygen不存在下面的限制

>   `<div>`、`<table>`、`<pre>`、`<p>` 等标签，必须在前后加上空行与其它内容区隔开，
>   还要求它们的开始标签与结尾标签不能用制表符或空格来缩进

您可以任意排列这些块标签

**2：**
Doxygen不会解释`<code>`和`</code>`所包含的内容，但会消除对应的前导空格，从而导致排版好的代码过于混乱，如果您需要在注释或者markdown中嵌入格式化过的代码，建议用`<pre>``</pre>`标签或者直接缩进4个空格

**3：**
Doxygen仅支持少量常见的标签形式，对于JavaScript代码或者其他标签（比如按钮），默认是当做纯文本来处理，并将JavaScript中所有特殊字符转义化，这样，插入的代码就无法生效

比如，我们希望在Markdown中插入一个按钮

    <button type="input" title="Test Button">Button</button>

Doxygen会将这句话转换为下面的形式

    &lt;button type="input" title="Test Button"&gt;Button&lt;/button&gt;

为了达到预定效果，我们需要添加JavaScript脚本来将插入的内容“反转义化”
替换代码如下：

    <script type="text/javascript" src="jquery.js"></script>

    <script>
    $(document).ready(function(e) {
        $('p').each(function(index, element) {
            var text = $(this).html();
            text = text.replace('$BEGIN$','');
            text = text.replace('$END$','');
            text = text.replace('&lt;','<');
            text = text.replace('&gt;','>');
            $(this).html(text);
        });
    });
    </script>

当然，我们需要将HTML代码改写为下面的形式

    $BEGIN$
    <button type="input" title="Test Button">Button</button>
    $END$

## Doxygen--Markdown拓展语法

### 表格

【语法规则】

Doxygen支持PHP风格的简单表格，如下所示

    First Header  | Second Header
    ------------- | -------------
    Content Cell  | Content Cell 
    Content Cell  | Content Cell 

表格的分割线由`-`和`|`组成，用于分割表格中的列和排，第一行称为表头，每个表有且仅有一个表头。其余的每行都是一个单独的行，行中的不同内容用`|`来分开。上图中的效果如下：

![Simple Table Demo-1](/images/2014/03/27/Table_1.jpg "Simple Table Demo-1")

稍微复杂一些的例子是

    First Header  | Second Header | Third Header
    ------------- | ------------- | ------------
    Content Cell  | Content Cell  | Content Cell 
    Content Cell  | Content Cell  | Content Cell 
    Content Cell  | Content Cell  | Content Cell 

输出效果如下

![Simple Table Demo-2](/images/2014/03/27/Table_2.jpg "Simple Table Demo-2")

当然，为了美观，可以在第一列和最后一列加上`|`符号，这不会影响输出效果，如下所示

    | First Header  | Second Header | Third Header |
    | ------------- | ------------- | ------------ |
    | Content Cell  | Content Cell  | Content Cell |
    | Content Cell  | Content Cell  | Content Cell |
    | Content Cell  | Content Cell  | Content Cell |

同时，Doxygen允许通过在`-----`首尾添加`:`的方式，来控制每列的对齐方式，如下所示

    第一列左对齐     第二列居中对齐  第三列右对齐

    | First Header  | Second Header | Third Header |
    | :------------ | :------------:| -----------: |
    | Content Cell  | Content Cell  | Content Cell |
    | Content Cell  | Content Cell  | Content Cell |
    | Content Cell  | Content Cell  | Content Cell |

输出结果如下所示

![Simple Table Demo-3](/images/2014/03/27/Table_3.jpg "Simple Table Demo-3")

语法很容易看懂，这里不做过多解释


【注意事项】

**1：** Doxygen仅支持非常简单的表格，如果您需要复杂表格，请通过：
    
    在word中创建，编辑表格，然后将转换后的HTML代码，贴到Markdown文件

或其他方法来是实现


### 插入代码块和语法高亮

【语法规则】

除了简单的使用` ` `来插入代码，常用的Markdown编译器还提供额外的指令来支持整块代码
插入的情况，常见的命令是

    ```

    Here Is Your Code

    ```

与此不太一样，Doxygen采用在代码块的前后插入N个`~`(N >= 3)方式来支持代码块，如下所示

    示例1

    ~~~

    Here Is Your Code

    ~~~

需要注意的是：代码前后`~`的数量要相同，比如下面的代码是错误的

    ~~~    这有3个~

    You Code is here

    ~~~~~~ 这有5个~

同时，Doxygen支持为特定编程语言设置语法高亮，如下所示

    ~~~{.代码语言}

    You Code is here

    ~~~

    或者

    ~~~代码语言

    You Code is here

    ~~~

比如下面代码用于高亮一段C语言代码

    示例2

    ~~~{.c}

    int func(int a,int b)
    {
        return a*b; 
    }

    ~~~

Doxygen支持的语言类型，请参考[这里](http://www.stack.nl/~dimitri/doxygen/manual/features.html)

【效果展示】

<br/>
**示例1：**通用代码块

![Format Code Demo 1](/images/2014/03/27/FormatCode_1.jpg "Format Code Demo")

<br/>
**示例2：**C语法高亮

![Format Code Demo 2](/images/2014/03/27/FormatCode_2.jpg "Format Code Demo")


### 创建标题ID

【语法规则】

如果我们为某个Markdown创建目录，便需要引用标题ID，但标准Markdown不支持直接为标题创建ID

一般情况下，我们采用直接插入HTML语法来为标题创建唯一的ID，如下所示

    *   [概述](#overview)
    *   [安装](#install)

    <h1 id="overview">概述</h1>
    <h2 id="install">安装</h2>

但这样写，不符合Markdown简介的精神，所以PHP为Markdown增加了标题ID属性，如下所示

    概述                {#overview}
    ========

    ## 安装 ##          {#install}

有了标题ID，我们便可以采用文内引用的方式来编写标题，如下所示

    示例1
    
    *   [概述](#overview)
    *   [安装](#install)

    概述                {#overview}
    ========

    ## 安装 ##          {#install}

Doxygen针对目录这种结构，专门提出了`[TOC]`命令，具体用法，请参考下一章节

【效果展示】

![Header ID Attribute](/images/2014/03/27/Header_ID_Attribute.jpg "Header ID Attribute")

【注意事项】

**1：** 标题ID仅适用于1-4级标题

**2：** `#`类型标题必须闭合，比如下面写法是错误的
    
    ## 安装           {#install}

**3：** `[Link text](#labelid)`这种写法仅适用于同一个文件（或同一个块）内的引用，如果要
跨文件引用，请将`#`改为`@`如下所示

    [Link text](@labelid)

**4：**如果希望将某个Markdown文件放到输出文档首页，请将该Markdown文件中首次出现的一级标题ID属性
设置为`index`或者`mainpage`


### 文档目录TOC命令

【语法规则】

Doxygen为了便于制作标题，特意提供了TOC这个命令，需要标题时，请在Markdown文件开始处增加
`[TOC]`指令，如下所示

    示例1

    *   [概述](#overview)
    *   [安装](#install)

    概述                {#overview}
    ========

    ## 安装 ##          {#install}

【效果展示】

**示例1：**增加目录

![Header ID Attribute](/images/2014/03/27/Header_ID_Attribute.jpg "Header ID Attribute")


【注意事项】

**0：**必须将`[TOC]`放到文章开始处

下面为错误写法

    概述        {#Overview}
    ========

    ## 安装 ##  {#Install}

    [TOC]

**1：**Markdown标题必须有ID属性，否则Doxygen不会生成目录

下面为错误写法

    [TOC]

    概述  
    ========

    ## 安装 ##

## 引用外部Markdown文件

很多情况下，我们需要在一个Markdown文件中引用另外一个Markdown文件，提供两种方式

1）直接引用markdown文件名  
2）引用文件标题ID

下面详细介绍：

**直接引用Markdown文件名**

Doxygen允许您在普通链接中直接引用markdown完整路径（包含文件名）的方式来引用外部Markdown文件，如下所示

    [显示名](完整Markdown文件路径)

这里的完整路径，可以是相对路径，也可以是绝对路径。

**注：**如果引用和被引用的markdown文件在同一个目录下，则直接写文件名即可，如下所示

    [This ](完整Markdown文件路径)

**引用文件标题ID**

默认情况下，Doxygen将Markdown文件名作为文档中的显示名，同时，Doxygen允许用户自己定义文档的显示名字，如下所示

    This is document show name
    ==========================

## Markdown与代码交互

Markdown中，我们也可以与代码进行交互，比如直接引用某个函数，点击后悔自动跳转到对应的函数文档页面

具体做法如下：

    \ref 需要引用的符号链接

比如我们需要引用`SystemInit`这个函数，可以这样写

    \ref SystemInit


## 结束语

以上是我对Doxygen中使用Markdown的总结，这里有很多坑，请特别注意我在文中标注**注意**的提示文字


在编写文档的过程中，参考了很多资料，在此表示感谢。如果您在阅读本文的过程中，发现错误或者发现某些文章段落不好理解，欢迎留言告诉我，我将及时纠正

{% blockquote Cedar, QQ:819280802 %}
Do one thing and do it well
{% endblockquote %}

##	参考资料

1.	[Doxygen文档主页](http://www.stack.nl/~dimitri/doxygen/manual/index.html)
2.	[Doxygen文档主页--Markdown支持页](http://www.stack.nl/~dimitri/doxygen/manual/markdown.html)
3.	[Markdown标准语法--中文版](https://gitcafe.com/riku/Markdown-Syntax-CN/blob/master/syntax.md)
4.	[Markdown标准语法--英文版](http://daringfireball.net/projects/markdown/syntax)
5.	[Markdown标准语法--中文入门教程](http://wowubuntu.com/markdown/basic.html)

## 常见Markdown编辑器

* **Windows 平台**
    * [MarkdownPad](http://markdownpad.com/)
    * [MarkPad](http://code52.org/DownmarkerWPF/)
* **Linux 平台**
    * [ReText](http://sourceforge.net/p/retext/home/ReText/)
* **Mac 平台**
    * [Mou](http://mouapp.com/)
* **在线编辑器**
    * [stackedit.io](https://stackedit.io/#)
    * [Markable.in](http://markable.in/)
    * [Dillinger.io](http://dillinger.io/)
* **浏览器插件**
    * [MaDe](https://chrome.google.com/webstore/detail/oknndfeeopgpibecfjljjfanledpbkog) (Chrome)
* **高级应用**
    * [Sublime Text 2](http://www.sublimetext.com/2)
    * [MarkdownEditing](http://ttscoff.github.com/MarkdownEditing/)
    * [SublineMarkdown教程](http://lucifr.com/2012/07/12/markdownediting-for-sublime-text-2/)
