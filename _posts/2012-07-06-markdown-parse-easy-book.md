---
layout: post
title: markdown简易语法
categories:
- tools
tags:
- markdown
- learn tips
---

<h2>最常用格式</h2>
<ul>
<li>空一行（两个回车）分段</li>
<li>行末加两个或多个空格才是真正的换行，否则正常的一个回车就像在 HTML 代码中一样，被当作空格处理</li>
<li>插入链接： <code>[链接文字](url)</code></li>
<li>图片跟链接很像，在前面加个叹号：<code>![alt 文字](图片 URL)</code></li>
</ul>
<p>段落和换行有什么区别？段落在生成的 HTML 代码中被一对 <code>&lt;p&gt;&lt;/p&gt;</code> 标签包含起来，而换行只是插入了一个 <code>&lt;br /&gt;</code> 标签。一般来说，网页设计给段落之间留的空白应该比行距大。</p>
<h2>其它格式</h2>
<p>下面会遇到一些语法需要在许多行前插入统一的缩进或特殊符号的，因此你需要一个非常舒服的<a href="http://qingbo.net/picky/509-column-editing.html">支持列编辑模式的文本编辑器</a>。</p>
<h3>内嵌 HTML</h3>
<p>由于内嵌 HTML 可以做 HTML 能做的任何事情，因此在用户可以自由输入的地方，需要禁用此功能，比如本站点的评论框。</p>
<ul>
<li>block level elements 像 p, div 之类的，需要前后各空一行（两个回车），并且开始和结束标签那一行的前面不能用空格或 Tab 缩进。</li>
<li>span level elements 如 a, img 可以在任何地方使用</li>
</ul>
<h3>标题</h3>
<p>用 1-6 个井号 (#) 开始一行表示这一行是标题，例如：</p>
<pre><code># 一级标题
## 二级标题
###### 六级标题
</code></pre>
<h3>blockquote</h3>
<p>用右尖括号 (<code>&gt;</code>) 表示 blockquote，你一定见过邮件中这样表示引用别人的内容。可以嵌套，可以包含其它的 Markdown 元素，例如：</p>
<pre><code>&gt; ## This is a header.
&gt;
&gt; 1.   This is the first list item.
&gt; 2.   This is the second list item.
&gt;
&gt; Here's some example code:
&gt;
&gt;     return shell_exec("echo $input | $markdown_script");
</code></pre>
<h3>列表</h3>
<p>HTML 列表分无序列表 (unordered list, ul) 和有序列表 (ordered list, ol) 两种。在 Markdown 中用星号、加号、减号开始一行表示无序列表，用数字开始一行表示有序列表。例如：</p>
<pre><code>*   Red
*   Green
*   Blue

1.  Bird
2.  McHale
3.  Parish
</code></pre>
<p>当然在有序列表中不必完全按照数字顺序标记，不过最好第一个条目使用数字 1. 列表的标记符号一般写在一行的开始，不过也可以在前面加最多三个空格 (如果加四个空格就表示是源代码了，见后文)。</p>
<h3>代码及代码块</h3>
<p>如果是在一段文字中插入一句代码，把代码用 (`) 符号包围起来即可。这个符号在键盘左上角，1 的左边，Tab 的上面。</p>
<p>如果插入一大段代码也很简单，在代码的每一行之前加四个空格。</p>
<h3>横线</h3>
<p>三个或以上星号、减号或者下划线单独放在一行即可生成一条横线 (horizontal rule, hr). 以下例子都是可以的：</p>
<pre><code>* * *
***
*****
- - -
---------------------------------------
</code></pre>
<h3>强调</h3>
<p>用星号或下划线来实现。两边分别放一个 * 或 _ 会生成 em 标签，放两个则生成 strong 标签。例如：</p>
<pre><code>*单星号*

_单下划线_

**双星号**

__双下划线__
</code></pre>
<p>会生成:</p>
<pre><code>&lt;em&gt;单星号&lt;/em&gt;

&lt;em&gt;单下划线&lt;/em&gt;

&lt;strong&gt;双星号&lt;/strong&gt;

&lt;strong&gt;双下划线&lt;/strong&gt;
</code></pre></div>