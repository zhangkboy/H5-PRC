# display:inline-block 元素之间空隙的产生原因和解决办法

## 原因

元素被当成行内元素排版的时候，元素之间的空白符（空格、回车换行等）都会被浏览器处理，根据 white-space 的处理方式（默认是 normal，合并多余空白），原来 HTML 代码中的回车换行被转成一个空白符，在字体不为 0 的情况下，空白符占据一定宽度，所以 inline-block 的元素之间就出现了空隙。这些元素之间的间距会随着字体的大小而变化，当行内元素 font-size:16px 时，间距为 8px。

## 尝试 1: 解决元素之间的空白符

```
<!-- 将所有子元素写在同一行 -->
<div class="parent">
  <div class="child">child1</div><div class="child">child2</div>
</div>
```

### 分析: 代码风格一保存立马换行, 不可行

## 尝试 2: 父元素中设置 font-size: 0，子元素上重置正确的 font-size

```
<div class="parent" style="font-size: 0px">
  <div class="child" style="font-size: 16px">child1</div>
  <div class="child" style="font-size: 16px">child2</div>
</div>
```

### 分析: inline-block 必须设置字体, 不然不显示, 还增加了代码量, 不可行

## 尝试 3: inline-block 元素添加样式 float:left

### 分析: 用 float 可能有高度塌陷问题

## 尝试 4: 子元素 margin 值为负数

```
.parent  .child {
  margin-left: -2px
}
```

### 分析: 间距与字体大小有关, 不同浏览器下间距也不同, 不可行

## 最优解，设置父元素，display:table 和 word-spacing

````

.parent{
display: table;
word-spacing:-1em; /_兼容其他浏览器，题主还未验证_/
}

```

````
