# 定义

BFC(Block formatting context)直译为"块级格式化上下文"。是一个独立的渲染区域，只有 Block-level box 参与， 它规定了内部的 Block-level Box 如何布局，并且与这个区域外部毫不相干

# 布局规则

- 内部的 Box 会在垂直方向一个一个的放置
- Box 垂直方向的距离由 margin 决定, 属于同一个 BFC 的两个相邻 Box 的 margin 会发生重叠
- 每个元素的 margin 左边与包含块 border box 的左边相接触, 即使存在浮动
- BFC 区域不会与 float box 重叠
- **一个独立的隔离容器, 容器里面的子元素不会影响到外面的元素, 外面的也不会影响到里面的**
- 计算 BFC 告高度, 浮动元素也计算

# 触发 BFC

- 根元素
- float 不为 none
- position 是 absolute 货 fixed
- display 是 inline-block 或 table-cell 或 table-caption 或 inline-flex
- overflow 不是 visible

# 示例一: 防止垂直 margin 重叠

```
<style>
    p {
    color: #f66;
    background: #fcc;
    width: 200px;
    line-height: 100px;
    text-align: center;
    margin: 40px;
    }
    .parent {
    overflow: hidden;
    }
</style>
<body>
    <p>AAA</p>
    <div class="parent">
        <p>BBB</p>
    </div>
</body>
```

_布局规则第二条: Box 垂直方向的距离由 margin 决定。属于同一个 BFC 的两个相邻 Box 的 margin 会发生重叠_

# 示例二: 清除内部浮动

```
<style>
    .parent {
        overflow: hidden;
        width: 200px;
    }
    .child {
        width: 100px;
        height: 100px;
        float: left
    }
</style>
<body>
    <div class="parent">
        <div class="child"></div>
        <div class="child"></div>
    </div>
</body>
```

_布局规则第六条:计算 BFC 的高度时，浮动元素也参与计算_

# 示例三: float 两栏布局

```
<style>
    body {
        width: 300px;
        position: relative;
    }

    .aside {
        width: 100px;
        height: 150px;
        float: left;
        background: #f66;
    }

    .main {
        height: 200px;
        background: #fcc;
    }
</style>
<body>
    <div class="aside"></div>
    <div class="main"></div>
</body>
```

_布局规则第四条:BFC 的区域不会与 float box 重叠。_
