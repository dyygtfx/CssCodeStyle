# CssCodeStyle
###css创作指南

---

[原文](https://github.com/csswizardry/CSS-Guidelines)

在参与规模庞大、历时漫长且参与人数众多的项目时，所有开发者遵守如下规则极为重要：

+ **保持 CSS 便于维护**
+ **保持代码清晰易懂**
+ **保持代码的可拓展性**

为了实现这一目标，我们要采用诸多方法。

本文档第一部分将探讨语法、格式以及分析 CSS 结构；第二部分将围绕方法论、思维框架以及编写与规划 CSS 的态度。

## 目录

**第一部分**
* [CSS 文档分析](#css-%E6%96%87%E6%A1%A3%E5%88%86%E6%9E%90)
  * [总则](#%E6%80%BB%E5%88%99)
  * [单一文件与多文件](#%E5%8D%95%E4%B8%80%E6%96%87%E4%BB%B6%E4%B8%8E%E5%A4%9A%E6%96%87%E4%BB%B6)
  * [目录](#%E7%9B%AE%E5%BD%95-1)
  * [区块标题](#%E5%8C%BA%E5%9D%97%E6%A0%87%E9%A2%98)
* [代码顺序](#%E4%BB%A3%E7%A0%81%E9%A1%BA%E5%BA%8F)
* [CSS 规则集分析](#css-%E8%A7%84%E5%88%99%E9%9B%86%E5%88%86%E6%9E%90)
* [命名规范](#%E5%91%BD%E5%90%8D%E8%A7%84%E8%8C%83)
  * [JavaScript 钩子](#javascript-%E9%92%A9%E5%AD%90)
  * [I18n](#i18n)
* [注释](#%E6%B3%A8%E9%87%8A)
  * [注释的拓展用法](#%E6%B3%A8%E9%87%8A%E7%9A%84%E6%8B%93%E5%B1%95%E7%94%A8%E6%B3%95)
    * [准修饰选择器](#%E5%87%86%E4%BF%AE%E9%A5%B0%E9%80%89%E6%8B%A9%E5%99%A8)
    * [代码标签](#%E4%BB%A3%E7%A0%81%E6%A0%87%E7%AD%BE)
    * [继承标记](#%E7%BB%A7%E6%89%BF%E6%A0%87%E8%AE%B0)

**第二部分**
* [编写 CSS](#%E7%BC%96%E5%86%99-css)
* [编写新组件](#%E7%BC%96%E5%86%99%E6%96%B0%E7%BB%84%E4%BB%B6)
* [面向对象 CSS](#%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1-css)
* [布局](#%E5%B8%83%E5%B1%80)
* [UI 尺寸](#ui-%E5%B0%BA%E5%AF%B8)
  * [字号](#%E5%AD%97%E5%8F%B7)
* [简写](#%E7%AE%80%E5%86%99)
* [ID](#id)
* [选择器](#%E9%80%89%E6%8B%A9%E5%99%A8)
  * [过修饰选择器](#%E8%BF%87%E5%BA%A6%E4%BF%AE%E9%A5%B0%E7%9A%84%E9%80%89%E6%8B%A9%E5%99%A8)
  * [选择器性能](#%E9%80%89%E6%8B%A9%E5%99%A8%E6%80%A7%E8%83%BD)
* [使用 CSS 选择器的目的](#%E4%BD%BF%E7%94%A8-css-%E9%80%89%E6%8B%A9%E5%99%A8%E7%9A%84%E7%9B%AE%E7%9A%84)
* [`!important`](#important)
* [魔数与绝对定位](#%E9%AD%94%E6%95%B0%E4%B8%8E%E7%BB%9D%E5%AF%B9%E5%AE%9A%E4%BD%8D)
* [条件判断](#%E6%9D%A1%E4%BB%B6%E5%88%A4%E6%96%AD)
* [Debugging](#debugging)
* [CSS 预处理器](#css-%E9%A2%84%E5%A4%84%E7%90%86%E5%99%A8)  

**第三部分**
* [css命名规范参考](#css-) 
 
---

## CSS 文档分析

无论编写什么文档，我们都应当尽力维持统一的风格，包括统一的注释、统一的语法与统一的命名规范。

### 总则

尽量将行宽控制在 80 字节以下。渐变（gradient）相关的语法以及注释中的 URL 等可以算作例外，毕竟这部分我们也无能为力。

我倾向于用 4 个空格而非 Tab 缩进，并且将声明拆分成多行。

### 单一文件与多文件

有人喜欢在一份文件文件中编写所有的内容，而我在迁移至 Sass 之后开始将样式拆分成多个小文件。这都是很好的做法。无论你选择哪种，下文的规则都将适用，而且如果你遵守这些规则的话你也不会遇到什么问题。这两种写法的区别仅仅在于目录以及区块标题。

### 目录

在 CSS 的开头，我会写一份目录，例如：

    /*------------------------------------*\
        $CONTENTS
    \*------------------------------------*/
    /**
     * CONTENTS............You’re reading it!
     * RESET...............Set our reset defaults
     * FONT-FACE...........Import brand font files
     */

这份目录可以告诉其他开发者这个文件中具体含有哪些内容。这份目录中的每一项都与其对应的区块标题相同。

如果你在维护一份单文件 CSS，对应的区块将也在同一文件中。如果你是在编写一组小文件，那么目录中的每一项应当对应相应的 @include 语句。

### 区块标题

目录应当对应区块的标题。请看如下示例：

    /*------------------------------------*\
        $RESET
    \*------------------------------------*/

区块标题前缀 `$` 可以让我们使用 [Cmd|Ctrl]+F 命令查找标题名的同时<strong>将搜索范围限制在区块标题中</strong>。

如果你在维护一份大文件，那么在区块之间空 5 行，如下：

    /*------------------------------------*\
        $RESET
    \*------------------------------------*/
    [Our
    reset
    styles]
    
    
    
    
    
    /*------------------------------------*\
        $FONT-FACE
    \*------------------------------------*/

在大文件中快速翻动时这些大块的空档有助于区分区块。

如果你在维护多份、以 @include 连接的 CSS 的话，在每份文件头加上标题即可，不必这样空行。

## 代码顺序

尽量按照特定顺序编写规则，这将确保你充分发挥 CSS 缩写中第一个 <i>C</i> 的意义：cascade，层叠。

一份规划良好的 CSS 应当按照如下排列：

1. **Reset** 万物之根源
2. **元素类型** 没有 class 的 `h1`、`ul` 等
3. **对象以及抽象内容** 最一般、最基础的设计模式
4. **子元素** 由对象延伸出来的所有拓展及其子元素
5. **修补** 针对异常状态

如此一来，当你依次编写 CSS 时，每个区块都可以自动继承在它之前区块的属性。这样就可以减少代码相互抵消的部分，减少某些特殊的问题，组成更理想的 CSS 结构。

关于这方面的更多信息，强烈推荐 Jonathan Snook 的 [SMACSS](http://smacss.com)。

## CSS 规则集分析

    [selector]{
        [property]:[value];
        [<- Declaration ->]
    }

    [选择器]{
        [属性]:[值];
        [<- 声明 ->]
    }

编写 CSS 样式时，我习惯遵守这些规则：

* class 名称以连字符（-）连接，除了下文提到的 BEM 命名法；
* 缩进 4 空格；
* 声明拆分成多行；
* 声明以相关性顺序排列，而非字母顺序；
* 有前缀的声明适当缩进，从而对齐其值；
* 缩进样式从而反映 DOM；
* 保留最后一条声明结尾的分号。

例如：

    .widget{
        padding:10px;
        border:1px solid #BADA55;
        background-color:#C0FFEE;
        -webkit-border-radius:4px;
           -moz-border-radius:4px;
                border-radius:4px;
    }
        .widget-heading{
            font-size:1.5rem;
            line-height:1;
            font-weight:bold;
            color:#BADA55;
            margin-right:-10px;
            margin-left: -10px;
            padding:0.25em;
        }

我们可以发现，`.widget-heading` 是 `.widget` 的子元素，因为前者比后者多缩进了一级。这样通过缩进就可以让开发者在阅读代码时快速获取这样的重要信息。

我们还可以发现 `.widget-heading` 的声明是根据其相关性排列的：`.widget-heading` 是行间元素，所以我们先添加字体相关的样式声明，接下来是其它的。

以下是一个没有拆分成多行的例子：

    .t10    { width:10% }
    .t20    { width:20% }
    .t25    { width:25% }       /* 1/4 */
    .t30    { width:30% }
    .t33    { width:33.333% }   /* 1/3 */
    .t40    { width:40% }
    .t50    { width:50% }       /* 1/2 */
    .t60    { width:60% }
    .t66    { width:66.666% }   /* 2/3 */
    .t70    { width:70% }
    .t75    { width:75% }       /* 3/4*/
    .t80    { width:80% }
    .t90    { width:90% }

在这个例子（来自[inuit.css’s table grid system](https://github.com/csswizardry/inuit.css/blob/master/inuit.css/partials/base/_tables.scss#L88)）中，将 CSS 放在一行内可以使得代码更紧凑。

## 命名规范

一般情况下我都是以连字符（-）连接 class 的名字（例如 `.foo-bar` 而非 `.foo_bar` 或 `.fooBar`），不过在某些特定的时候我会用 BEM（Block, Element, Modifier）命名法。

<abbr title="Block, Element, Modifier">BEM</abbr> 命名法可以使得选择器更规范，更清晰，更具语义。

该命名法按照如下格式：

    .block{}
    .block__element{}
    .block--modifier{}

其中：

* `.block` 代表某个基本的抽象元素；
* `.block__element` 代表 `.block` 这一整体的一个子元素；
* `.block--modifier` 代表 `.block` 的某个不同状态。

打个比方：

    .person{}
    .person--woman{}
        .person__hand{}
        .person__hand--left{}
        .person__hand--right{}

这个例子中我们描述的基本元素是一个人，然后这个人可能是一个女人。我们还知道人拥有手，这些是人体的一部分，而手也有不同的状态，如同左手与右手。

这样我们就可以根据亲元素来划定选择器的命名空间并传达该选择器的职能，这个选择器是一个子元素（`__`）还是亲元素的不同状态（`--`）？

由此，`.page-wrapper` 是一个独立的选择器。这是一个符合规范的命名，因为它不是其它元素的子元素或其它状态；然而 `.widget-heading` 则与其它对象有关联，它应当是 `.widget` 的子元素，所以我们应当将其重命名为 `.widget__heading`。

BEM 命名法虽然不太好看，而且相当冗长，但是它使得我们可以通过名称快速获知元素的功能和元素之间的关系。与此同时，BEM 语法中的重复部分非常有利于 gzip 的压缩算法。

无论你是否使用 BEM 命名法，你都应当确保 class 命名得当，力保一字不多、一字不少；将元素命名抽象化以提高复用性（例如 `.ui-list`，`.media`）。由此延伸出去的元素命名则要尽量精准（例如 `.user-avatar-link`）。不用担心 class 名的数量或长度，因为写得好的代码 gzip 也能有效压缩。

### HTML 中的 class

为了确保易读性，在 HTML 标记中用两个空格隔开 class 名，例如：

    <div class="foo--bar  bar__baz">

增加的空格应当可以使得在使用多个 class 时更易阅读与定位。

### JavaScript 钩子

**千万不要把 CSS 样式用作 JavaScript 钩子。**把 JS 行为与样式混在一起将无法对其分别处理。

如果你要把 JS 和某些标记绑定起来的话，写一个 JS 专用的 class。简单地说就是划定一个前缀 `.js-` 的命名空间，例如 `.js-toggle`，`.js-drag-and-drop`。这意味着我们可以通过 class 同时绑定 JS 和 CSS 而不会因为冲突而引发麻烦。

    <th class="is-sortable  js-is-sortable">
    </th>

上面的这个标记有两个 class，你可以用其中一个来给这个可排序的表格栏添加样式，用另一个添加排序功能。

### I18n

虽然我（该 CSS Guideline 文档原作者 Harry Roberts）是个英国人，而且我一向拼写 <i>colour</i> 而非 <i>color</i>，但是为了追求统一，我认为在 CSS 中用美式拼法更佳。CSS 以及其它多数语言都是以美式拼法编写，所以如果在 `.colour-picker{}` 中写 `color:red` 就缺乏统一性。我以前主张同时用两种拼法，例如：

    .color-picker,
    .colour-picker{
    }

但是我最近参与了一份规模庞大的 Sass 项目，这个项目中有许多的颜色变量（例如 `$brand-color`，`$highlight-color` 等等），每个变量要维护两种拼法实在辛苦，要查找并替换时也需要两倍的工作量。

所以为了统一，把所有的 class 与变量都以你参与的项目的惯用拼法命名即可。

## 注释

我使用行宽不超过 80 字节的块状注释：

    /**
     * This is a docBlock style comment
     * 
     * This is a longer description of the comment, describing the code in more
     * detail. We limit these lines to a maximum of 80 characters in length.
     * 
     * We can have markup in the comments, and are encouraged to do so:
     * 
       <div class=foo>
           <p>Lorem</p>
       </div>
     * 
     * We do not prefix lines of code with an asterisk as to do so would inhibit
     * copy and paste.
     */


    /**
     * 这是一个文档块（DocBlock）风格的注释。
     *
     * 这里开始是描述更详细、篇幅更长的注释正文。当然，我们要把行宽控制在 80 字以内。
     *
     * 我们可以在注释中嵌入 HTML 标记，而且这也是个不错的办法：
     *
        <div class=foo>
            <p>Lorem</p>
        </div>
     *
     * 如果是注释内嵌的标记的话，在它前面不加星号，否则会被复制进去。
     */

在注释中应当尽量详细描述代码，因为对你来说清晰易懂的内容对其他人可能并非如此。每写一部分代码就要专门写注释以详解。

### 注释的拓展用法

注释有许多很先进的用法，例如：

* 准修饰选择器
* 代码标签
* 继承标记

#### 准修饰选择器

你应当避免过分修饰选择器，例如如果你能写 `.nav{}` 就尽量不要写 `ul.nav{}`。过分修饰选择器将影响性能，影响 class 复用性，增加选择器私有度。这些都是你应当竭力避免的。

不过有时你可能希望告诉其他开发者 class 的使用范围。以 `.product-page` 为例，这个 class 看起来像是一个根容器，可能是 `html` 或者 `body` 元素，但是仅凭 `.product-page` 则无法判断。

我们可以在选择器前加上准修饰（即将前面的类型选择器注释掉）来描述我们规划的 class 作用范围：

    /*html*/.product-page{}

这样我们就能准确获知该 class 的作用范围而不会影响复用性。

其它例子如：

    /*ol*/.breadcrumb{}
    /*p*/.intro{}
    /*ul*/.image-thumbs{}

这样我们就能在不影响代码私有度的前提下获知 class 作用范围。

#### 代码标签

如果你写了一个新规则的话，可以在它上面加上标签，例如：

    /**
     * ^navigation ^lists
     */
    .nav{}
    
    /**
     * ^grids ^lists ^tables
     */
    .matrix{}

这些标签可以使得其他开发者快速找到相关代码。如果一个开发者需要查找和列表相关的部分，他只要搜索 `^lists` 就能快速定位到 `.nav`，`.matrix` 以及其它相关部分。

#### 继承标记

将面向对象的思路用于 CSS 编写的话，你经常能找到两部分 CSS 密切相关（其一为基础，其一为拓展）却分列两处。我们可以用继承标记来在原元素和继承元素之间建立紧密联系。这些在注释中的写法如下：

在元素的基本样式中：

    /**
     * Extend `.foo` in theme.css
     */
     .foo{}

在元素的拓展样式中：

    /**
     * Extends `.foo` in base.css
     */
     .bar{}

这样一来我们就能在两块相隔很远的代码间建立紧密联系。

---

## 编写 CSS

之前的章节主要探讨如何规划 CSS，这些都是易于量化的规则。本章将探讨更理论化的东西，也将探讨我们的态度与方法。

## 编写新组件

编写新组件时，要在着手处理 CSS <strong>之前</strong>写好 HTML 部分。这可以令你准确判断哪些 CSS 属性可以继承，避免重复浪费。

先写标记的话，你就可以关注数据、内容与语义，在这之后再添加需要的 class 和 CSS 样式。

## 面向对象 CSS

我以面向对象 CSS 的方式写代码。我把组件分成结构（对象）与外观（拓展）。正如以下分析：

    .room{}
    
    .room--kitchen{}
    .room--bedroom{}
    .room--bathroom{}

我们在屋子里有许多房间，它们都有共同的部分：它们都包含地板、天花板、墙壁和门。这些共享的部分我们可以放到一个抽象的 `.room{}` class 中。不过我们还有其它与众不同的房间：一个厨房可能有地砖，卧室可能有地毯，洗手间可能没有窗户但是卧室会有，每个房间的墙壁颜色也许也会不一样。面向对象 CSS 的思路使得我们把相同部分抽象出来组成结构部分，然后用更具体的 class 来拓展这些特征并添加特殊的处理方法。

所以比起编写大量的特殊模块，应当努力找出这些模块中重复的设计模式并将其抽象出来，写成一个可以复用的 class，将其用作基础然后编写其它拓展模块的特殊情形。

当你要编写一个新组件时，将其拆分成结构和外观。编写结构部分时用最通用 class 以保证复用性，编写外观时用更具体的 class 来添加设计方法。

## 布局

所有组件都不要声明宽度，而由其亲元素或格栅系统来决定。

**坚决不要**声明高度。高度应当仅仅用于尺寸已经固定的东西，例如图片和 CSS Sprite。在 `p`，`ul`，`div` 等元素上不应当声明高度。如果需要的话可以写 `line-height`，这个更加灵活。

格栅系统应当当作书架来理解。是它们容纳内容，而不是把它们本身当成内容装起来，正如你先搭起书架再把东西放进去。比起声明它们的尺寸，把格栅系统和元素的其它属性分来开处理更有助于布局，也使得我们的前端工作更高效。

你在格栅系统上不应当添加任何样式，他们仅仅是为布局而用。在格栅系统内部再添加样式。在格栅系统中任何情况下都不要添加盒模型相关属性。

## UI 尺寸

我用很多方法设定 UI 尺寸，包括百分比，`px`，`em`，`rem` 以及干脆什么都不用。

理想情况下，格栅系统应当用百分比设定。如上所述，因为我用格栅系统来固定栏宽和页宽，所以我可以不用理会元素的尺寸。

我用 rem 定义字号，并且辅以 px 以兼容旧浏览器。这可以兼具 em 和 px 的优势。下面是一个非常漂亮的 Sass Mixin，假设你在别处声明了基本字号（base-font-size）的话，用它就可以生成 rem 以及兼容旧浏览器的 px。

    @mixin font-size($font-size){
        font-size:$font-size +px;
        font-size:$font-size / $base-font-size +rem;
    }

我只在已经固定尺寸的元素上使用 px，包括图片以及尺寸已经用 px 固定的 CSS Sprite。

### 字号

我会定义一些与格栅系统原理类似的 class 来声明字号。这些 class 可以用于双重标题分级，关于这点请阅读 [Pragmatic, practical font-sizing in CSS](http://csswizardry.com/2012/02/pragmatic-practical-font-sizing-in-css)。

## 简写

**CSS 简写应当谨慎使用。**
    
编写像 `background:red;` 这样的属性的确很省事，但是你这么写的意思其实是同时声明 `background-image:none; background-position:top left; background-repeat: repeat; background-color:red;`。虽然大多数时候这样不会出什么问题，但是哪怕只出一次问题就值得考虑要不要放弃简写了。这里应当改为 `background-color:red;`。

类似的，像 `margin:0;` 这样的声明的确简洁清爽，但是还是应当<strong>尽量写清楚</strong>。如果你只是想修改底边边距，就要具体一些，写成 `margin-bottom:0;`。

反过来，你需要声明的属性也要写清楚，不要因为简写而波及其它属性。例如如果你只想改掉底部的 `margin`，那就不要用会把其它边距也清零的 `margin:0`。

简写虽然是好东西，但是注意切勿滥用。

## ID

在我们开始处理选择器之前，牢记这句话：

**在 CSS 里坚决不要用 ID。**

在 HTML 里 ID 可以用于 JS 以及锚点定位，但是在 CSS 里只要用 class，一个 ID 也不要用。

Class 的优势在于复用性，而且私有度也并不高。私有度非常容易导致问题，所以将其降低就尤为重要。ID 的私有度是 class 的 **255** 倍，所以在 CSS 中坚决不要使用。

## 选择器

务必保持选择器简短高效。

通过页面元素位置而定位的选择器并不理想。例如 `.sidebar h3 span{}` 这样的选择器就是定位过于依赖相对位置，所以把 span 移到 h3 和 sidebar 外面时就很难保持其样式。

结构复杂的选择器将会影响性能。选择器结构越复杂（如 `.sidebar h3 span` 为三层，`.content ul p a` 是四层），浏览器的消耗就越大。

尽量使得样式不依赖于其定位，尽量保持选择器简洁清晰。

作为一个整体，选择器应当尽量简短（例如只有一层结构），但是 class 名则不应当过于简略，例如 `.user-avatar` 就远比 `.usr-avt` 好。

**牢记：**class 无所谓是否语义化；应当关注它们是否合理。不要强调 class 名要符合语义，而要注重使用合理且不会过时的名称。

### 过度修饰的选择器

由前文所述，过度修饰的选择器并不理想。

过度修饰的选择器是指像 `div.promo` 这样的。很可能你只用 `.promo` 也能得到相同的效果。当然你可能偶尔会需要用元素类型来修饰 class（例如你写了一个 `.error` 而且想让它在不同的元素类型中显示效果不一样，例如 `.error{ color:red; }` `div.error{ padding:14px;}`），但是大多数时候还是应当尽量避免。

再举一个修饰过度的选择器例子，`ul.nav li a{}`。如前文所说，我们马上就可以删掉 `ul` 因为我们知道 `.nav` 是个列表，然后我们就可以发现 `a` 一定在 `li` 中，所以我们就能将这个选择器改写成 `.nav a{}`。

### 选择器性能

虽然浏览器性能日渐提升，渲染 CSS 速度越来越快，但是你还是应当关注效率。使用间断、没有嵌套的选择器，不把全局选择器（`*{}`）用作核心选择器，避免使用日渐复杂的 CSS3 新选择器可以避免这样的问题。

译注，核心选择器：浏览器解析选择器为从右向左的顺序，最右端的元素是样式生效的元素，是为核心选择器。

## 使用 CSS 选择器的目的

比起努力运用选择器定位到某元素，更好的办法是直接给你想要添加样式的元素直接添加一个 class。我们以 `.header ul{}` 这样一个选择器为例。

假定这个 `ul` 就是这个网站的全站导航，它位于 header 中，而且目前为止是 header 中唯一的 `ul` 元素。`.header ul{}` 的确可以生效，但是这样并不是好方法，它很容易过时，而且非常晦涩。如果我们在 header 中再添加一个 `ul` 的话，它就会套用我们给这个导航部分写的样式，哪怕我们设想的不是这个效果。这意味着我们要么要重构许多代码，要么给后面的 `ul` 新写许多样式来抵消之前的影响。

你的选择器必须符合你要给这个元素添加样式的原因。思考一下，<strong>「我定位到这个元素，是因为它是 `.header` 下的 `ul`，还是因为它是我的网站导航？」</strong>这将决定你应当如何使用选择器。

确保你的核心选择器不是类型选择器，也不是高级对象或抽象选择器。例如你在我们的 CSS 中肯定找不到诸如 `.sidebar ul{}` 或者 `.footer .media{}` 这样的选择器。

表达清晰：直接找到你要添加样式的元素，而非其亲元素。不要想当然地认为 HTML 不会改变。<strong>用 CSS 直接命中你需要的元素，而非投机取巧。</strong>

完整内容请参考我的文章 [Shoot to kill; CSS selector intent](http://csswizardry.com/2012/07/shoot-to-kill-css-selector-intent/)

## `!important`

只在起辅助作用的 class 上用 `!important`。用 `!important` 提升优先级也可以，例如如果你要让某条规则<strong>一直</strong>生效的话，可以用 `.error{ color:red!important; }`。

避免主动使用 `!important`。例如 CSS 写得很复杂时不要用它来取巧，要好好整理并重构之前的部分，保持选择器简短并且避免用 ID 将效果拔群。

## 魔数与绝对定位

魔数（Magic Number）是指那些「凑巧有效果」的数字，这东西非常不好，因为它们只是治标不治本而且缺乏拓展性。

例如 `.dropdown-nav li:hover ul{ top:37px; }` 把下拉菜单移动下来远非良策，因为这里的 37px 就是个魔数。37px 会生效的原因是因为这时 `.dropbox-nav` 碰巧高 37px 而已。

这时你应该用 `.dropdown-nav li:hover ul{ top:100%; }`，也即无论 `.dropbox-down` 多高，这个下拉菜单都会往下移动 100%。

每当你要在代码中放入数字的时候，请三思而行。如果你能用一个关键字（例如  `top:100%` 意即「从上面拉到最下面」）替换之，或者有更好的解决方法的话，就尽量避免直接出现数字。

你在 CSS 中留下的每一个数字，都是你许下而不愿遵守的承诺。

## 条件判断

专门为 IE 写的样式基本上都是可以避免的，唯一需要为 IE 专门处理的是为了处理 IE 不支持的内容（例如 PNG）。

简而言之，如果你重构 CSS 的话，所有的布局和盒模型都不用额外兼容 IE。也就是说你基本上不用 `<!--[if IE 7]> element{ margin-left:-9px; } < ![endif]-->` 或者类似的兼容 IE 的写法。 

## Debugging

如果你要解决 CSS 问题的话，<strong>先把旧代码拿掉再写新的</strong>。如果旧的 CSS 中有问题的话，写新代码是解决不了的。

把 CSS 代码和 HTML 部分删掉，直到没有 BUG 为止，然后你就知道问题出在哪里了。

有时候写上一个 `overflow:hidden` 或者其它能把问题藏起来的代码的确效果立竿见影，但是 overflow 方面可能根本就没问题。所以<strong>要治本，而不是单纯治标</strong>。

## CSS 预处理器

我用 Sass。使用时应当<strong>灵活运用</strong>。用 Sass 可以令你的 CSS 更强大，但是不要嵌套得太复杂。在 Vanilla CSS 中，只在必要的地方用嵌套即可，例如：

    .header{}
    .header .site-nav{}
    .header .site-nav li{}
    .header .site-nav li a{}

这样的写法在普通 CSS 里完全用不到。以下为<strong>不好的</strong> Sass 写法：

    .header{
        .site-nav{
            li{
                a{}
            }
        }
    }


## CSS命名规范

### 1.1 为什么要制定CSS命名规范  

统一的命名规范，便于多人开发维护时代码统一，减少项目沟通和交接的成本，增加代码的语义化。
### 1.2 CSS命命规则  
1. 样式类名全部用小写，首字符必须是字母，禁止数字或其他特殊字符。由以字母开头的小写字母（a-z）、数字（0-9）、连字符（-）组成。  

2. 可以是单个单词，也可以是组合单词，要求能够描述清楚模块和元素的含义，使其具有语义化。避免使用 123456…red,blue,left,right之类的（如颜色、字号大小等）矢量命名，如class="left_news"、class="2" ，以避免当状态改变时名称失去意义。尽量用单个单词简单描述class名称。  
3. 双单词或多单词组合方式：形容词-名词、命名空间-名次、命名空间-形容词-名词。例如：news-list、mod-feeds、mod-my-feeds、cell-title  
 
### 1.3 Class 和 id的使用方法  
把id留给后台开发和JS使用，除此之外页面的page id(如首页的外层需要一个ID id="page-index")，页面结构（header main footer）允许用id命名。其他禁止id使用在样式表CSS命名中，一律使用class命名。
### 1.4 命名空间  
在编码思想上，我们可以将页面拆分成不同的层级（布局、模块、元件）。
什么是CSS命名空间？  
通过统一的命名规范定义命名的范围，成为CSS  class & id命名空间。
布局: 以语义化的单词layout作为命名空间，例如主栏布局命名 layout-main，只改变layout-命名空间后面的命名，layout始终保留。布局的命名空间为layout-xxx。  
模块：页面是由一个或多个模块组成，模块的英文单词是module，规范简写成mod，如新闻模块mod-news，照片展示模块mod-photo-show。模块的命名空间为mod-xxx 。
元件：元件是属于模块内部的，也可以说模块是由元件和它内部的自有元素组成。如用户照片信息元件cell-user-photo。元件的命名空间为cell-xxx 。  
### 1.5 通用命名  
##### (1)页面框架命名，一般具有唯一性，推荐用ID命名  

头部 header    
主体 main  
脚部  footer   
容器  wrapper  
侧栏  side-bar      
栏目  column  
布局  layout        
##### (2)模块结构命名    

模块(如：新闻模块) mod (mod-news)    
标题栏 title  
内容  content  
次级内容    sub-content  
##### (3)导航结构命名  
导航  nav   
主导航 main-nav  
子导航 sub-nav  
顶部导航    top-nav  
菜单  menu      
子菜单 sub-menu  
##### (3)小元件命名    
##### (4)一般元素命名(class)   
二级  sub   
面包屑 breadcrumb     
标志  logo     
广告  bner(禁用banner或ad)    
登陆  login     
注册  register/reg  
搜索  search    
加入  join  
状态  status    
按钮  btn  
滚动  scroll    
标签页 tab  
文章列表    list      
短消息 msg/message  
当前的 current   
提示小技巧   tips  
图标  icon      
注释  note  
指南  guide      
服务  service  
热点  hot   
新闻  news  
下载  download      
投票  vote  
合作伙伴  partner   
友情链接    link  
版权  copyright     
演示  demo  
下拉框 select   
摘要  summary  
翻页  pages     
主题风格  themes    
设置  set      
成功  suc    
按钮  btn     
文本  txt    
颜色  color/c     
背景  bg    
边框  border/bor      
居中  center    
上   top/t    
下   bottom/b  
左   left/l    
右   right/r  
添加  add   
删除  del  
间隔  sp    
段落  p  
弹出层 pop  
公共  global/gb  
操作  op    
密码  pwd  
透明  tran      
信息  info  
重点  hit   
预览  pvw  
单行输入框 input    
首页  index  
日志  blog      
相册  photo  
留言板 guestbook      
用户  user  
确认  confirm  
取消  cancel  
报错  error           
##### (5)全局皮肤样式  
文字颜色(命名空间text_xxx)  
text-c1, text-c2,text-c3……  
背景颜色(命名空间bg -xxx)  
bg-c1,bg-c2,bg-c3……  
边框颜色(命名空间border-xxx)  
border-c1,border-c2,border-c3……  

如果你用 Sass 的话，尽量这么写：

    .header{}
    .site-nav{
        li{}
        a{}
    }
