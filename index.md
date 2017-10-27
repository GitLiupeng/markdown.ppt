---

layout: ribbon

style: |

    #Cover h2 {
        margin:30px 0 0;
        color:#FFF;
        text-align:center;
        font-size:70px;
        }
    #Cover p {
        margin:10px 0 0;
        text-align:center;
        color:#FFF;
        font-style:italic;
        font-size:40px;
        }
---

# Sass语法使用

*Sass 是一个 CSS 的扩展，它在 CSS 语法的基础上，允许您使用变量 (variables), 嵌套规则 (nested rules), 混合 (mixins), 导入 (inline imports) 等功能，令 CSS 更加强大与优雅。使用 Sass 以及 Compass 样式库 有助于更好地组织管理样式文件，以及更高效地开发项目。*

![](pictures/cover.jpg)

## 特色

1.完全兼容 CSS3
2.在 CSS 语言的基础上增加变量(variables)、嵌套 (nesting)、混合 (mixins) 等功能
3.通过函数进行颜色值与属性值的运算
4.提供 控制指令等高级功能
5.自定义输出格式

## 语法格式 {#Cover}

1.SCSS:本PPT所介绍的格式 , 这种格式仅在 CSS3 语法的基础上进行扩展，这意味着每个CSS样式表是一个同等的SCSS文件，这种语法的样式表文件需要以 .scss 作为拓展名。
2.SASS:缩进语法，使用缩进而不是花括号来表示选择器的嵌套，用换行而不是分号来分隔属性，以 .sass 作为扩展名。

## 嵌套规则

    #main {
        width: 97%;
        p, div {
            font-size: 2em;
            a { font-weight: bold; }
        }
        pre { font-size: 3em; }
    }

## 嵌套属性

    .funky {
        font: {
            family: fantasy;
            size: 30em;
            weight: bold;
        }
    }

## 引用父选择器:&

    #main {
        color: black;
        &-sidebar {
            border: 1px solid;
        }
        &:hover { color: red; }
    }

## 注释

    /* This comment is several lines long.
     * it will appear in the CSS output. */
    body { color: black; }
    // These comments are only one line long each.
    // They won't appear in the CSS output,
    a { color: green; }
    $version: "1.2.3";
    /*version #{$version}*/

## 变量

    $width: 1em;
    #main {
        $width: 5em !global;
        width: $width;
    }
    #sidebar {
        width: $width;
    }

## 数据类型

1.数字 (例如： 1.2, 13, 10px)
2.文本字符串，带引号字符串和不带引号字符串(例如："foo", 'bar', baz)
3.颜色 (例如：blue, #04a3f9, rgba(255, 0, 0, 0.5))
4.布尔值 (例如： true, false)
5.空值 (例如： null)
6.值列表 (list)，用空格或逗号分隔 (例如： 1.5em 1em 0 2em, Helvetica, Arial, sans-serif)
7.maps ，从一个值映射到另一个 (例如： (key1: value1, key2: value2))

## 字符串

    @mixin firefox-message($selector) {
        body.firefox #{$selector}:before {
            content: "Hi, Firefox users!";
        }
    }

    @include firefox-message(".header");

## 列表

    $linkColor:  #08c #333 !default;//第一个值为默认值，第二个鼠标滑过值
    a{
        color:nth($linkColor,1);
        &:hover{
            color:nth($linkColor,2);
        }
    }

## 集合

    $headings: (h1: 2em, h2: 1.5em, h3: 1.2em);
    @each $header, $size in $headings {
        #{$header} {
            font-size: $size;
        }
    }

## 运算

    p {
        $width: 1000px;
        width: $width/2;            // 使用了变量, 作为除法
        color: #010203 + #040506;
        cursor: e + -resize;
    }
    p:before {
        content: "Foo " + Bar;
        font-family: sans- + "serif";
    }

## 插值

    $name: foo;
    $attr: border;
    p.#{$name} {
        #{$attr}-color: blue;
    }

## @import

    @import "foo.scss";
    @import "foo";

    #main {
        @import "example";
    }

## @extend

    .error {
      border: 1px #f00;
      background-color: #fdd;
    }
    .seriousError {
      @extend .error;
      border-width: 3px;
    }
    .criticalError {
      @extend .seriousError;
      position: fixed;
    }

## @if

    $type: monster;
    p {
        @if $type == ocean {
            color: blue;
        } @else if $type == matador {
            color: red;
        } @else if $type == monster {
            color: green;
        } @else {
            color: black;
        }
    }

## @for

    @for $i from 1 through 3 {
          .item-#{$i} { width: 2em * $i; }
    }

    @for $i from 1 to 3 {
          .item-#{$i} { width: 2em * $i; }
    }

## @each

    @each $animal in puma, sea-slug, egret, salamander {
        .#{$animal}-icon {
            background-image: url('/images/#{$animal}.png');
        }
    }

    @each $header, $size in (h1: 2em, h2: 1.5em, h3: 1.2em) {
      #{$header} {
            font-size: $size;
      }
    }

## @while

    $i: 6;
    @while $i > 0 {
        .item-#{$i} { width: 2em * $i; }
        $i: $i - 2;
    }

## @mixin

    @mixin large-text($size) {
        font: {
            family: Arial;
            size: $size;
            weight: bold;
        }
    }
    .page-title {
        @include large-text(30px);
        padding: 4px;
        margin-top: 10px;
    }

## 函数

    $grid-width: 40px;
        $gutter-width: 10px;

    @function grid-width($n) {
        @return $n * $grid-width + ($n - 1) * $gutter-width;
    }

    #sidebar { width: grid-width(5); }
