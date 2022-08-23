---
title: 2022/8/15-2022/8/20组内分享
categories: 分享
tags: 
  - Sass
  - vue
sharedBy: myy
---

## 2022/08/15分享

### Sass预处理语言中@mixin和@include的使用

@mixin可以定义一个重复使用的样式；@include可以将@mixin引入

~~~ css
@mixin common($width, $size, $color) { //可以带上默认值 $width：20px, $size: 10px
    width: $width;
    height: $width;
}
.box {
    @include radius(20px, 20px)
}
~~~

## 2022/08/16分享

1. 数字，字符串类型转换
{% asset_img 1.png %}

2. 巧用空值合并
{% asset_img 2.png %}

3. 通过!!进行布尔转换
{% asset_img 3.png %}

## 2022/08/17分享

{% asset_img 4.png %}
推荐使用label这种写法，下面这种写法，在切换语言的时候，多次点击已经选中的值，可能会出现语言混乱（比如该展示英文，实际出现了中文）
