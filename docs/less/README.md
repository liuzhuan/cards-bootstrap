# 使用 Less

[Less.js](http://lesscss.org/)

在学习 less 过程中，[Less-To-CSS Playground](http://lesscss.org/less-preview/) 是一个很棒的在线转译工具。

Less 是 CSS 的扩展语言。它增加了以下特性：

变量

```less
@width: 10px;
@height: @width + 10px;

#header {
    width: @width;
    height: @height;
}
```

混入（*Mixins*）

```less
.bordered {
    border-top: dotted 1px black;
    border-bottom: solid 2px black;
}

#menu a {
    color: #111;
    .bordered();
}

.post a {
    color: red;
    .bordered();
}
```

嵌套

```less
#header {
    color: black;
    .navigation {
        font-size: 12px;
    }
    .logo {
        width: 300px;
    }
}
```

```less
.clearfix {
    display: block;
    zoom: 1;
    
    &:after {
        content: " ";
        display: block;
        font-size: 0;
        height: 0;
        clear: both;
        visibility: hidden;
    }
}
```

嵌套 At-Rules 和冒泡

```less
.component {
    width: 300px;
    @media (min-width: 768px) {
        width: 600px;
        @media (min-resolution: 192dpi) {
            background-image: url(/img/retina2x.png);
        }
    }
    
    @media (min-width: 1280px) {
        width: 800px;
    }
}
```

操作符

```less
@conversion-1: 5cm + 10mm; // => 6cm
@conversion-2: 2 - 3cm - 5mm; // => -1.5cm

@incompatible-units: 2 + 5px - 3cm; // => -106.3858px

@base: 5%;
@filler: @base * 2; // => 10%;
@other: @base + @filler; // => 15%

@base: 2cm * 3mm; // => 6cm

@color: #224488 / 2; // => #112244
background-color: #112244 + #111; // => 223355
```

`calc()` 例外

v3.0.0 之后，为了兼容 CSS，`calc()` 不被转译：

```less
@var: 50vh / 2;
width: calc(50% + (@var - 20px)); // => calc(50% + (25vh - 20px))
```

转译

```less
@min768: ~"(min-width: 768px)";
.element {
    @media @min768 {
        font-size: 1.2em;
    }
}

// v3.5+ 不需要转译
@min768: (min-width: 768px);
.element {
    @media @min768 {
        font-size: 1.2rem;
    }
}
```

函数

```less
@base: #f04615;
@width: 0.5;

.class {
    width: percentage(@width);
    color: saturate(@base, 5%);
    background-color: spin(lighten(@base, 25%), 8);
}
```

To Be Continued