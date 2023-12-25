# 使用 float 父元素高度塌陷问题

例如:

```
     <style>
      .content {
        background-color: red;
      }
      h1,
      p {
        float: left;
      }
    </style>

    <div class="content">
      <h1>float</h1>
      <p>aaaaaaaaaaa</p>
      <p>
        bbbbbbbbbbb
      </p>
    </div>
```

## 问题: 子元素使用 float 后, 父元素的高度变成 0px

_分析: 元素浮动之后, 会脱离文档流, 周围的元素会重新排列, 当父元素没有足够的高度, 又没有其他非浮动的子元素的时候,父元素的高度就会塌陷为 0_

## 解决 1: 父元素底部增加一行代码, 清除浮动, 如下

```
<div style="clear:both;"></div>
```

缺点: 增加了没啥意义的空标签, 不建议

## 解决 2: 使用 CSS 中的 after 伪元素

给父元素设置新的 class: clearfix 后设置 css

```
  .clearfix:after{
        content: ".";
        display: block;
        height: 0px;
        clear: both;
        visibility: hidden;
   }
```

这个类似于第一种, 不过是通过 after 伪元素给父元素末尾增加一个看不见的块元素, 并设置了元素的 clear:both, 高度为 0, 不可见

## 解决 3: 利用 BFC 来给父元素增加 CSS

```
.content{
       overflow:auto;
  }
```

除此之外 display:table-cell;或 display:table-caption;或 display:inline-block;或 position:fixed;或 position:absolute 这些也可以，它们可以清除浮动，其实是因为触发了 BFC（块级格式化上下文）

## 解决 4: 大师级别的-尼古拉斯大师方法

```
.clearfix:after,
.clearfix:before{
      content: " ";
      display: table;
}
.clearfix:after{
      clear: both;
}
```

**现在大多数人都会采用最后一种方式来清除浮动**

**另一个较为现代的方案是使用 display 属性的 flow-root 值。它可以无需小技巧来创建块格式化上下文（BFC），在使用上没有副作用。**

```
.content {
  display: flow-root;
}
```
