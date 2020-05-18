
### 1.标题

**代码**

注：# 后面保持空格

```bash
# h1
## h2
### h3
#### h4
##### h5
###### h6
####### h7      // 错误代码
######## h8     // 错误代码
######### h9    // 错误代码
########## h10  // 错误代码

```

**演示**

# h1

## h2

### h3

#### h4

##### h5

###### h6

####### h7  
######## h8  
######### h9  
########## h10

----------

### 2.分级标题

**代码**  
注：`=` `-` 最少可以只写一个，兼容性一般

```undefined
一级标题
======================
二级标题
---------------------

```

**演示**

![](https://upload-images.jianshu.io/upload_images/6912209-c969047ea76e86b3.png?imageMogr2/auto-orient/strip|imageView2/2/w/568/format/webp)

----------

### 3.TOC

注：根据标题生成目录，兼容性一般

**代码**


[TOC]


**演示**

![](https://upload-images.jianshu.io/upload_images/6912209-0c9a604cd6f84d8c.png?imageMogr2/auto-orient/strip|imageView2/2/w/354/format/webp)

----------

### 4.引用

**代码1(单行式)**

```undefined
> hello world!

```

**演示**

> hello world!

**代码2(多行式)**

```undefined
> hello world!
hello world!
hello world!    

```

或者

```undefined
> hello world!
> hello world!
> hello world!

```

**演示**

相同的结果

> hello world!  
> hello world!  
> hello world!

**代码3(多层嵌套)**

```ruby
> aaaaaaaaa
>> bbbbbbbbb
>>> cccccccccc

```

**演示**

> aaaaaaaaa
> 
> > bbbbbbbbb
> > 
> > > cccccccccc

----------

### 5.行内标记

注：用 ` 标记**代码块将变成一行**

**代码**

```go
标记之外`hello world`标记之外

```

**演示**

标记之外`hello world`标记之外

**错误代码**  
注：不同平台错误略有差异

```xml
 标记之外 ` 
< div>   
    < div></div>
    < div></div>
    < div></div>
< /div>
`标记之外

```

**演示**

![](//upload-images.jianshu.io/upload_images/6912209-6e436a12165b5469.png?imageMogr2/auto-orient/strip|imageView2/2/w/551/format/webp)

----------

### 6.代码块

注：与上行距离一空行

**代码1(```)**

注：用` ``` `生成块

```xml
```
<div>   
    <div></div>
    <div></div>
    <div></div>
</div>
```

```

**演示**

```xml
<div>   
    <div></div>
    <div></div>
    <div></div>
</div>

```

**代码2(Tab)**

注： Tab缩进

```xml
我是文字……

    <div>   
        <div></div>
        <div></div>
        <div></div>
    </div>

```

**演示**

```xml
<div>   
    <div></div>
    <div></div>
    <div></div>
</div>

```

**代码3(自定义语法)**  
注：根据不同的语言配置不同的代码着色

```dart
```javascript
var num = 0;
for (var i = 0; i < 5; i++) {
    num+=i;
}
console.log(num);
```

```

**演示**

```javascript
var num = 0;
for (var i = 0; i < 5; i++) {
    num+=i;
}
console.log(num);

```

----------

### 7.插入链接

**代码1(内链式)**  
注：`{:target="_blank"}`跳转方式兼容性一般 ，多数第三方平台不支持跳转

```ruby
[百度1](http://www.baidu.com/" 百度一下"){:target="_blank"}   

```

**演示**

[百度1](http://www.baidu.com/%22%E7%99%BE%E5%BA%A6%E4%B8%80%E4%B8%8B%22)

**代码2(引用式)**

```csharp
[百度2][2]{:target="_blank"}
[2]: http://www.baidu.com/   "百度二下"

```

**演示**

[百度2](http://www.baidu.com/%22%E7%99%BE%E5%BA%A6%E4%B8%80%E4%B8%8B%22)

----------

### 8.插入图片

**代码1(内链式)**

```json
[图片上传失败...(image-90880b-1542510791300)]

```

**演示**

![](//upload-images.jianshu.io/upload_images/6912209-8c53b79a706bb7c2.png?imageMogr2/auto-orient/strip|imageView2/2/w/273/format/webp)

**代码2(引用式)**

```csharp
![name][01]
[01]: ./01.png '描述'

```

**演示**

![](//upload-images.jianshu.io/upload_images/6912209-2b1e8871d7bf2d6e.png?imageMogr2/auto-orient/strip|imageView2/2/w/273/format/webp)

----------

### 9.插入图片带有链接

**代码**

```csharp
[[图片上传失败...(image-f83b77-1542510791300)]](http://www.baidu.com){:target="_blank"}       // 内链式

[[图片上传失败...(image-4dc956-1542510791300)]][5]{:target="_blank"}                      // 引用式
[5]: http://www.baidu.com

```

**演示**

![](//upload-images.jianshu.io/upload_images/6912209-1c3d07c7077c76c0.png?imageMogr2/auto-orient/strip|imageView2/2/w/273/format/webp)

[](http://www.baidu.com)

[

![](//upload-images.jianshu.io/upload_images/6912209-1c3d07c7077c76c0.png?imageMogr2/auto-orient/strip|imageView2/2/w/273/format/webp)

][5]  
[5]: [http://www.baidu.com](http://www.baidu.com)

----------

### 10.视频插入

注：Markdown 语法是不支持直接插入视频的  
普遍的做法是 插入HTML的 iframe 框架，通过网站自带的分享功能获取，如果没有可以尝试第二种方法  
第二是伪造播放界面，实质是插入视频图片，然后通过点击跳转到相关页面

**代码1**  
注：多数第三方平台不支持插入`<iframe>`视频

![](//upload-images.jianshu.io/upload_images/6912209-29337f2896bf4629.png?imageMogr2/auto-orient/strip|imageView2/2/w/621/format/webp)

youku

```xml
<iframe height=498 width=510 src='http://player.youku.com/embed/XMjgzNzM0NTYxNg==' frameborder=0 'allowfullscreen'></iframe>

```

**演示**

![](//upload-images.jianshu.io/upload_images/6912209-d11325d111b86cc1.png?imageMogr2/auto-orient/strip|imageView2/2/w/508/format/webp)

**代码2**

```csharp
[[图片上传失败...(image-49aefe-1542510791300)]](http://v.youku.com/v_show/id_XMjgzNzM0NTYxNg==.html?spm=a2htv.20009910.contentHolderUnit2.A&from=y1.3-tv-grid-1007-9910.86804.1-2#paction){:target="_blank"}

```

**演示**

![](//upload-images.jianshu.io/upload_images/6912209-d11325d111b86cc1.png?imageMogr2/auto-orient/strip|imageView2/2/w/508/format/webp)

[](http://v.youku.com/v_show/id_XMjgzNzM0NTYxNg==.html?spm=a2htv.20009910.contentHolderUnit2.A&from=y1.3-tv-grid-1007-9910.86804.1-2#paction)

----------

### 11.序表

**代码1(有序)**

注：序列`.`后 保持空格

```undefined
1. one
2. two
3. three

```

**演示**

1.  one
2.  two
3.  three

**代码2(无序)**

```undefined
* one
* two
* three

```

**演示**

-   one
-   two
-   three

**代码3(序表嵌套)**

```undefined
1. one
    1. one-1
    2. two-2
2. two 
    * two-1
    * two-2

```

**演示**

1.  one
    1.  one-1
    2.  two-2
2.  two
    -   two-1
    -   two-2

----------

**代码4(序表嵌套代码块)**  
注：换行+两个Tab

```csharp
* one

    var a = 10;     // 与上行保持空行并 递进缩进

```

**演示：**

-   one
    
    ```csharp
      var a = 10;
    
    ```
    

----------

### 12.任务列表

注：兼容性一般 要隔开一行

**代码**

```css
这是文字……

- [x] 选项一
- [ ] 选项二  
- [ ]  [选项3]

```

**演示**

![](//upload-images.jianshu.io/upload_images/6912209-5d37b0a39ce101c9.png?imageMogr2/auto-orient/strip|imageView2/2/w/342/format/webp)

----------

### 13.表情

注：兼容一般

![](//upload-images.jianshu.io/upload_images/6912209-35a94b525d1ec313.png?imageMogr2/auto-orient/strip|imageView2/2/w/273/format/webp)

[表情代码地址](https://www.webpagefx.com/tools/emoji-cheat-sheet/'GitHub')

----------

### 14.表格

注： `:` 代表对齐方式 ,** `:` 与 `|` 之间不要有空格**，否则对齐会有些不兼容

**代码1**

```ruby
|    a    |       b       |      c     |
|:-------:|:------------- | ----------:|
|   居中  |     左对齐    |   右对齐   |
|=========|===============|============|

```

**演示**

a

b

c

居中

左对齐

右对齐

=========

===============

============

----------

**代码2(简约写法)**

```ruby
a  | b | c  
:-:|:- |-:
    居中    |     左对齐      |   右对齐    
============|=================|=============

```

**演示**

a

b

c

居中

左对齐

右对齐

============

=================

=============

**代码3(特殊表格)**

注：一般对合并单元格，以及其他特殊格式表格，markdown 是无能为力的  
所以常规的做法是使用HTML标签，但是这样的编写效率极低。  
但是有了这款工具的话，所有问题都迎刃而解。

在线生成HTML代码 [Tables Generator](http://www.tablesgenerator.com/) (国外的站)

![](//upload-images.jianshu.io/upload_images/6912209-46aac2b114b995ec.png?imageMogr2/auto-orient/strip|imageView2/2/w/1113/format/webp)

Tables Generator

**演示**

![](//upload-images.jianshu.io/upload_images/6912209-5e14abef7e65830d.png?imageMogr2/auto-orient/strip|imageView2/2/w/409/format/webp)

----------

### 15.支持内嵌CSS样式

**代码**

```xml
<p style="color: #AD5D0F;font-size: 30px; font-family: '宋体';">内联样式</p>

```

**演示**

![](//upload-images.jianshu.io/upload_images/6912209-a6e8fb087f500f2c.png?imageMogr2/auto-orient/strip|imageView2/2/w/276/format/webp)

----------

### 16.语义标记

描述

效果

代码

斜体

_斜体_

`*斜体*`

斜体

_斜体_

`_斜体_`

加粗

**加粗**

`**加粗**`

加粗+斜体

**_加粗+斜体_**

`***加粗+斜体***`

加粗+斜体

**_加粗+斜体_**

`**_加粗+斜体_**`

删除线

删除线

`~~删除线~~`

----------

### 17.语义标签

描述

效果

代码

斜体

<i>斜体</i>

`<i>斜体</i>`

加粗

<b>加粗</b>

`<b>加粗</b>`

强调

<em>强调</em>

`<em>强调</em>`

上标

Za

`Z<sup>a</sup>`

下标

Za

`Z<sub>a</sub>`

键盘文本

![](//upload-images.jianshu.io/upload_images/6912209-9f4177c5bfb69ab0.png?imageMogr2/auto-orient/strip|imageView2/2/w/47/format/webp)

`<kbd>Ctrl</kbd>`

换行

----------

### 18.格式化文本

**保持输入排版格式不变**  
注：对内含标签需要破坏结构才能显示

**代码**

```xml
<pre>
hello world 
         hi
  hello world 
</pre>

```

**演示**

<pre>  
hello world  
hi  
hello world  
</pre>

**错误解决方法**  
注：标签内部添加空格 或者 **直接使用` ``` `标记来处理**  
**代码1(插入空格)**

```xml
<pre>
    < div>   
        < div>< /div>
        < div>< /div>
        < div>< /div>
    < /div>
</pre>

```

**演示**

<pre>  
< div>  
< div>< /div>  
< div>< /div>  
< div>< /div>  
< /div>  
</pre>

**代码2( ` ``` ` 代码块标记)**

```xml
```
<div>   
    <div></div>
    <div></div>
    <div></div>
</div>
```

```

**演示**

```xml
<div>   
    <div></div>
    <div></div>
    <div></div>
</div>

```

----------

### 19.公式 {#1}

注：1个$左对齐，2个居中

**代码**

```ruby
$$ x \href{why-equal.html}{=} y^2 + 1 $$
$ x = {-b \pm \sqrt{b^2-4ac} \over 2a}. $

```

**演示**

![](//upload-images.jianshu.io/upload_images/6912209-09ce088470cefc30.png?imageMogr2/auto-orient/strip|imageView2/2/w/544/format/webp)

----------

### 20.分隔符

注：最少三个 `---` 或 `***`或 `* * *`

**代码**

```undefined
***
---
* * *

```

**演示**

----------

----------

----------

### 21.脚注

**代码**

```csharp
Markdown[^1]
[^1]: Markdown是一种纯文本标记语言        // 在文章最后面显示脚注

```

**演示**

Markdown[[1]](#fn1)

----------

### 22.锚点

**代码**  
注：只有**标题**支持锚点， 跳转目录方括号后 保持空格

```csharp
[公式标题锚点](#1)

### [需要跳转的目录] {#1}    // 方括号后保持空格

```

**演示**

[公式标题锚点](#1)

----------

### 23.定义型列表

注：解释型定义  
**代码**

```csharp
Markdown 
:   轻量级文本标记语言，可以转换成html，pdf等格式  //  开头一个`:` + `Tab` 或 四个空格

代码块定义
:   代码块定义……

        var a = 10;         // 保持空一行与 递进缩进

```

**演示**

![](//upload-images.jianshu.io/upload_images/6912209-f8681b8080fbc65f.png?imageMogr2/auto-orient/strip|imageView2/2/w/585/format/webp)

----------

### 24.自动邮箱链接

**代码**

```css
<xxx@outlook.com>

```

**演示**

[xxx@outlook.com](mailto:xxx@outlook.com)

----------

### 25.流程图

**代码1**

```php
```flow                     // 流程
st=>start: 开始|past:> http://www.baidu.com // 开始
e=>end: 结束              // 结束
c1=>condition: 条件1:>http://www.baidu.com[_parent]   // 判断条件
c2=>condition: 条件2      // 判断条件
c3=>condition: 条件3      // 判断条件
io=>inputoutput: 输出     // 输出
//----------------以上为定义参数-------------------------

//----------------以下为连接参数-------------------------
// 开始->判断条件1为no->判断条件2为no->判断条件3为no->输出->结束
st->c1(yes,right)->c2(yes,right)->c3(yes,right)->io->e
c1(no)->e                   // 条件1不满足->结束
c2(no)->e                   // 条件2不满足->结束
c3(no)->e                   // 条件3不满足->结束
```

```

**演示**

![](//upload-images.jianshu.io/upload_images/6912209-972af6417eb7db1e.png?imageMogr2/auto-orient/strip|imageView2/2/w/635/format/webp)

**代码详解**  
流程图分为两个部分： **定义参数** 然后 **连接参数**

**定义示例：**

```dart
tag=>type: content:>url         // 形参格式 
st=>start: 开始:>http://www.baidu.com[blank]  //实参格式

```

注：** `st=>start: 开始` 的`：`后面保持空格**

形参

实参

含义

tag

st

标签 (可以自定义)

=>

=>

赋值

type

start

类型 (6种类型)

content

开始

描述内容 (可以自定义)

:>url

`http://www.baidu.com[blank]`

链接与跳转方式 **兼容性很差**

6种类型

含义

start

启动

end

结束

operation

程序

subroutine

子程序

condition

条件

inputoutput

输出

**连接示例：**

```rust
st->c1(yes,right)->c2(yes,right)->c3(yes,right)->io->e
开始->判断条件1为no->判断条件2为no->判断条件3为no->输出->结束

```

形参

实参

含义

->

->

连接

condition

c1

条件

(布尔值,方向)

(yes,right)

如果满足向右连接，4种方向：right ，left，up ，down 默认为：down

注：operation (程序); subroutine (子程序) ;condition (条件)，都可以在括号里加入连接方向。

```swift
operation(right) 
subroutine(left)
condition(yes,right)    // 只有条件 才能加布尔值

```

----------

**代码2**

注：添加样式和url跳转 需要添加第三方的脚本  
实际效果很差，使用起来麻烦，意义不大

```php
```flow                             // 流程
st=>start: 启动|past:>http://www.baidu.com[blank] // 开始
e=>end: 结束                      // 结束
op1=>operation: 方案一             // 运算1
sub2=>subroutine: 方案二|approved:>http://www.baidu.com[_parent]  // 运算2
sub3=>subroutine: 重新制定方案        // 运算2
cond1=>condition: 行不行？|request  // 判断条件1
cond2=>condition: 行不行？          // 判断条件2
io=>inputoutput: 结果满意           // 输出

// 开始->方案1->判断条件->
st->op1->cond1
// 判断条件1为no->方案2->判断条件2为no->重新制定方案->方案1
cond1(no,right)->sub2->cond2(no,right)->sub3(right)->op1
cond1(yes)->io->e       // 判断条件满足->输出->结束
cond2(yes)->io->e       // 判断条件满足->输出->结束
```

```

**演示**

![](//upload-images.jianshu.io/upload_images/6912209-b7f44683e3b3e60e.png?imageMogr2/auto-orient/strip|imageView2/2/w/564/format/webp)

**作者地址：[flowchart.js](https://github.com/adrai/flowchart.js)**

**一般普遍支持的效果**

![](//upload-images.jianshu.io/upload_images/6912209-c276eb80f3e93081.png?imageMogr2/auto-orient/strip|imageView2/2/w/580/format/webp)

----------

### 26.时序图

**代码1**

```go
```sequence
A->>B: 你好
Note left of A: 我在左边     // 注释方向，只有左右，没有上下
Note right of B: 我在右边
B-->A: 很高兴认识你
```

```

**演示**

![](//upload-images.jianshu.io/upload_images/6912209-784ce9bb7beb6672.png?imageMogr2/auto-orient/strip|imageView2/2/w/393/format/webp)

**代码详解**

注：`A->>B: 你好` 后面可以不写文字，但是一定要在最后加上`：`  
Note left of A 代表注释在A的左边

符号

含义

`-`

实线

`>`

实心箭头

`--`

虚线

`>>`

空心箭头

**代码2**

```rust
    ```sequence
    起床->吃饭: 稀饭油条
    吃饭->上班: 不要迟到了
    上班->午餐: 吃撑了
    上班->下班:
    Note right of 下班: 下班了
    下班->回家:
    Note right of 回家: 到家了
    回家-->>起床:
    Note left of 起床: 新的一天
    ```

```

**演示**

![](//upload-images.jianshu.io/upload_images/6912209-f109a13fcf7e2ccb.png?imageMogr2/auto-orient/strip|imageView2/2/w/577/format/webp)

### 27.生成侧边栏扩展

注：生成侧边栏一般是插入JS，再就是模板,  
总体来说，很是麻烦，效果一般，不作详解。

作者仓库：[i5ting_ztree_toc](https://github.com/i5ting/i5ting_ztree_toc)

![](//upload-images.jianshu.io/upload_images/6912209-4d15bbf4a613ced4.png?imageMogr2/auto-orient/strip|imageView2/2/w/742/format/webp)

精简版：作者博客[HaleyPKU](http://blog.csdn.net/haleypku/article/details/51226704)

#### 总结：常用标记

标记

Markdown 语法

斜体

`*italic*`

粗体

`**bold**`

图片

`![Image Title](http://xxx.png)`

链接

`[Link Text](http://xxx.com)`

内联代码

`` `code` ``

块级代码

` ```code block``` `

引用

`> Here is a quote block`

分隔符

`----` 或 `*****`

标题 1

`# Heading 1`

标题 2

`## Heading 2`

标题 3

`### Heading 3`

标题 4

`#### Heading 4`

#### Markdown编写工具

[Typora：https://typora.io](https://typora.io/)

![](//upload-images.jianshu.io/upload_images/6912209-54579c9a1271cc0f.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

  
  
作者：欧薇娅  
链接：https://www.jianshu.com/p/b03a8d7b1719  
来源：简书  
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
<!--stackedit_data:
eyJoaXN0b3J5IjpbOTI5MDA2MTQwLC00MzM0MzcyOTJdfQ==
-->