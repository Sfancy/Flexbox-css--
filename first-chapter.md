# Flexbox
## 1. 引言
http://blog.csdn.net/whqet/article/details/45154977
原文地址 [A Visual Guide to CSS3 Flexbox Properties](https://scotch.io/tutorials/a-visual-guide-to-css3-flexbox-properties)

## 2. 正文
### 2.1 引入
Flexbox 布局官方称为[CSS Flexible Box Layout Module](http://www.w3.org/TR/css-flexbox/)是一个 CSS3 新的布局模块，用于实现容器里项目的对齐、方向、排序（即使在项目大小位置、动态生成的情况）。flex 容器最大的特性在于，能够修改子元素的宽度和高度，以满足在不同尺寸屏幕下的如意分布。
### 2.2 基础
flexbox 模型，flex 布局由父容器（flex container）和它的子元素（flex items）组成。
![flex](https://cask.scotch.io/2015/04/CSS3-Flexbox-Model.jpg)

访问 [flexbox model 官方文档](https://www.w3.org/TR/css-flexbox/#box-model) 来了解详情。

到[caniuse](http://caniuse.com/#search=flex)了解浏览器兼容情况详情。

本文中的用到的一些术语的表达约定如下

> 1. flex-container-弹性容器
> 2. flex-item-弹性子元素
> 3. main axis-主轴
> 4. cross axis-侧轴

### 2.3 使用

```html
<!DOCTYPE html>
<html>
<head>
<style> 

.flex-container {
	display: -webkit-flex;
    display: flex;
    width: 400px;
    height: 250px;
    background-color: lightgrey;
}

.flex-item {
    background-color: cornflowerblue;
    width: 100px;
    height: 100px;
    margin: 10px;
}
</style>
</head>
<body>
	<div class="flex-container">
  <div class="flex-item">flex item 1</div>
  <div class="flex-item">flex item 2</div>
  <div class="flex-item">flex item 3</div> 
</div>
</body>
</html>
```
使用 flexbox 只需要在父元素上设置 `display` 属性即可。

```css
.flex-container {
	display: -webkit-flex; /*Safari*/
	display: flex;
}
```
如果想让它以内联方式显示，则

```css
.flex-container {
	display: -webkit-inline-flex; /*Safari*/
	display: inline-flex;
}
```
> 注意：仅仅需要在父元素上设置这一个属性即可，它的子元素会自动变成 flex items。

有很多方式分组 flexbox 的所有属性，我发现最容易理解的方式是分成两组，一组为弹性容器的属性，另一组为弹性子元素的属性，接下来我们按这种方式来一一解析。

### 2.4 弹性容器（flex container）属性
### 2.4.1 flex-direction
该属性通过设置 flex container 主坐标轴方向影响子元素(flex item)如何在容器中排布。我们可以设置两个主要的方向水平和垂直方向。

默认值： `row`

|值|描述|
|-|-|
|`row`|弹性子元素会自左向右水平排列|
|`row-reverse`|弹性子元素会自右向左水平排列|
|`column`|弹性子元素会自上而下竖直排列|
|`column-reverse`|弹性子元素会自下而上竖直排列|

```css
.flex-container {
	-webkit-flex-direction: row; /* Safari */
	flex-direction: row;
}
```

使用 `row` 方向，弹性子元素会自左向右水平排列。
![flexbox-flex-direction-row](https://cask.scotch.io/2015/04/flexbox-flex-direction-row.jpg)

使用 `row-reverse` 方向，弹性子元素会自右向左水平排列。
![flexbox-flex-direction-row-reverse](https://cask.scotch.io/2015/04/flexbox-flex-direction-row-reverse.jpg)

使用 `column` 方向，弹性子元素会自上而下竖直排列。
![flexbox-flex-direction-column](https://cask.scotch.io/2015/04/flexbox-flex-direction-column.jpg)

使用 `column-reverse` 方向，弹性子元素会自下而上竖直排列。
![flexbox-flex-direction-column-reverse](https://cask.scotch.io/2015/04/flexbox-flex-direction-column-reverse.jpg)

> Note： `row` 和 `row-reverse` 是基于书写顺序的，所以在 `rtl` 环境下将会反置。

### 2.4.2 flex-wrap
flexbox 最初的理念是保持弹性容器的子元素在一行中。`flex-wrap` 属性控制当子元素 items 超出弹性容器范围是是否换行，以及新行的方向。

默认值： `nowrap`

|值|描述|
|-|-|
|`no-wrap`|弹性子元素将会在一行显示，默认的子元素会缩减以适应弹性容器的宽度|
|`wrap`|如果需要的话，弹性子元素将会自左向右、自上而下地多行显示|
|`wrap-reverse`|如果需要的话，弹性子元素将会自左向右、自下而上地多行显示|

```css
.flex-container {
	-webkit-flex-wrap: nowrap; /* Safari */
	flex-wrap: nowrap;
}
```

![flexbox-flex-wrap-nowrap](https://cask.scotch.io/2015/04/flexbox-flex-wrap-nowrap.jpg)

![flexbox-flex-wrap-wrap](https://cask.scotch.io/2015/04/flexbox-flex-wrap-wrap.jpg)

![flexbox-flex-wrap-wrap-reverse](https://cask.scotch.io/2015/04/flexbox-flex-wrap-wrap-reverse.jpg)

> Note：这些属性也是基于书写顺序的，所以在 `rtl` 环境会反置。

### 2.4.3 flex-flow
`flex-flow` 是 `flex-direction` 和 `flex-wrap` 属性的快捷方式。

默认值：`row nowrap`

```css
.flex-container {
  -webkit-flex-flow: <flex-direction> || <flex-wrap>; /* Safari */
  flex-flow: <flex-direction> || <flex-wrap>;
}
```

### 2.4.4 justify-content
`justify-content` 属性在弹性子元素未占用主轴所有空间时，设置水平对齐的方式。

|值|描述|
|-|-|
|`flex-start`|默认值；弹性子元素位于弹性容器开始位置|
|`flex-end`|弹性子元素位于弹性容器末端位置|
|`center`|弹性子元素在弹性容器中居中对齐|
|`space-between`|弹性子元素之间等间距对齐，首尾元素与弹性容器边缘对齐|
|`space-around`|弹性子元素之间等间距对齐，包括首尾元素|

```css
.flex-container {
  -webkit-justify-content: flex-start; /* Safari */
  justify-content: flex-start;
}
```

![flexbox-justify-content-flex-start](https://cask.scotch.io/2015/04/flexbox-justify-content-flex-start.jpg)

![flexbox-justify-content-flex-end](https://cask.scotch.io/2015/04/flexbox-justify-content-flex-end.jpg)

![flexbox-justify-content-center](https://cask.scotch.io/2015/04/flexbox-justify-content-center.jpg)

![flexbox-justify-content-space-between](https://cask.scotch.io/2015/04/flexbox-justify-content-space-between.jpg)

![flexbox-justify-content-space-around](https://cask.scotch.io/2015/04/flexbox-justify-content-space-around.jpg)

### 2.4.5 align-items
`align-items` 属性在弹性子元素未占用侧轴所有空间时，设置垂直对齐的方式。

|值|描述|
|-|-|
|`stretch`|默认值；弹性子元素伸缩以占用弹性容器侧轴整个高度|
|`flex-start`|弹性子元素处于弹性容器顶部|
|`flex-end`|弹性子元素处于弹性容器底部|
|`center`|弹性容器子元素在弹性容器中垂直居中|
|`baseline`|弹性子元素位于弹性容器的基线位置|

```css
.flex-container {
  -webkit-align-items: stretch; /* Safari */
  align-items: stretch;
}
```

![flexbox-align-items-stretch](https://cask.scotch.io/2015/04/flexbox-align-items-stretch.jpg)

![flexbox-align-items-flex-start](https://cask.scotch.io/2015/04/flexbox-align-items-flex-start.jpg)

![flexbox-align-items-flex-end](https://cask.scotch.io/2015/04/flexbox-align-items-flex-end.jpg)

![flexbox-align-items-center](https://cask.scotch.io/2015/04/flexbox-align-items-center.jpg)

![flexbox-align-items-baseline](https://cask.scotch.io/2015/04/flexbox-align-items-baseline.jpg)

> Note: Read more details about how baselines are calculated [here](https://www.w3.org/TR/css-flexbox/#flex-baselines).

### align-content
The align-content property aligns a flex container’s lines within the flex container when there is extra space in the cross-axis, similar to how justify-content aligns individual items within the main-axis.

值：
```css
.flex-container {
  -webkit-align-content: stretch; /* Safari */
  align-content:         stretch;
}
```
Flex items are displayed with distributed space after every row of flex items
![flexbox-align-content-stretch](https://cask.scotch.io/2015/04/flexbox-align-content-stretch.jpg)

```css
.flex-container {
  -webkit-align-content: flex-start; /* Safari */
  align-content:         flex-start;
}
```
Flex items are stacked toward the cross start of the flex container
![flexbox-align-content-flex-start](https://cask.scotch.io/2015/04/flexbox-align-content-flex-start.jpg)

```css
.flex-container {
  -webkit-align-content: flex-end; /* Safari */
  align-content:         flex-end;
}
```
Flex items are stacked toward the cross end of the flex container
![flexbox-align-content-flex-end](https://cask.scotch.io/2015/04/flexbox-align-content-flex-end.jpg)

```
.flex-container {
  -webkit-align-content: center; /* Safari */
  align-content:         center;
}
```
Rows of flex items are stacked in the center of the cross axis of the flex container
![flexbox-align-content-center](https://cask.scotch.io/2015/04/flexbox-align-content-center.jpg)

```css
.flex-container {
  -webkit-align-content: space-between; /* Safari */
  align-content:         space-between;
}
```
Rows of flex items are displayed with equal spacing between them, first and last rows are aligned to the edges of the flex container
![flexbox-align-content-space-between](https://cask.scotch.io/2015/04/flexbox-align-content-space-between.jpg)

```css
.flex-container {
  -webkit-align-content: space-around; /* Safari */
  align-content:         space-around;
}
```
Flex items are displayed with equal spacing around every row of flex items.
![flexbox-align-content-space-around](https://cask.scotch.io/2015/04/flexbox-align-content-space-around.jpg)

Default value: stretch

> Note: This property has only effect when the flex container has multiple lines of flex items. If they are placed in single line this property has no effect on the layout.


## Note for flex containers
- all of the `column-*` properties have no effect on a flex container.
- the `::first-line` and `::first-letter` pseudo-elements do not apply to flex containers.

## Flexbox item properties

## Order
The order property controls the order in which children of a flex container appear inside the flex container. By default they are ordered as initially added in the flex container.

Value
```css
.flex-item {
  -webkit-order: <integer>; /* Safari */
  order:         <integer>;
}
```
Flex items can be reordered with this simple property, without restructuring the HTML code
![](https://cask.scotch.io/2015/04/flexbox-order.jpg)
默认值： 0

## flex-grow
This property specifies the flex grow factor, which determines how much the flex item will grow relative to the rest of the flex items in the flex container when positive free space is distributed.

Value
```css
.flex-item {
  -webkit-flex-grow: <number>; /* Safari */
  flex-grow:         <number>;
}
```
If all flex items have same value for flex-grow than all items have same size in the container
![](https://cask.scotch.io/2015/04/flexbox-flex-grow-1.jpg)
The second flex item takes up more space relative to the size of the other flex items
![](https://cask.scotch.io/2015/04/flexbox-flex-grow-2.jpg)
Default value: 0

Note: Negative numbers are invalid.

### flex-shrink
The flex-shrink specifies the flex shrink factor, which determines how much the flex item will shrink relative to the rest of the flex items in the flex container when negative free space is distributed.

Value
```css
.flex-item {
  -webkit-flex-shrink: <number>; /* Safari */
  flex-shrink:         <number>;
}
```
By default all flex items can be shrunk, but if we set it to 0 (don’t shrink) they will maintain the original size
![](https://cask.scotch.io/2015/04/flexbox-flex-shrink.jpg)
Default value: 1

Note: Negative numbers are invalid.

### flex-basis
This property takes the same values as the width and height properties, and specifies the initial main size of the flex item, before free space is distributed according to the flex factors.

Values:
```css
.flex-item {
  -webkit-flex-basis: auto | <width>; /* Safari */
  flex-basis:         auto | <width>;
}
```
flex-basis is specified for the 4th flex item and dictates the initial size of the element
![](https://cask.scotch.io/2015/04/flexbox-flex-basis.jpg)

Default value: auto

Note: There is a naming issue with the auto value which will be resolved in future.

### flex

This property is the shorthand for the flex-grow, flex-shrink and flex-basis properties. Among other values it also can be set to auto (1 1 auto) and none (0 0 auto).

```css
.flex-item {
  -webkit-flex: none | auto | [ <flex-grow> <flex-shrink>? || <flex-basis> ]; /* Safari */
  flex:         none | auto | [ <flex-grow> <flex-shrink>? || <flex-basis> ];
}
```
Default value: 0 1 auto

Note: W3C encourages to use the flex shorthand rather than the separate component properties, as the shorthand correctly resets any unspecified components to accommodate common uses.

### align-self

This align-self property allows the default alignment (or the one specified by align-items) to be overridden for individual flex items. Refer to align-items explanation for flex container to understand the available values.

Values:

```css
.flex-item {
  -webkit-align-self: auto | flex-start | flex-end | center | baseline | stretch; /* Safari */
  align-self: auto | flex-start | flex-end | center | baseline | stretch;
}
```
The 3rd and 4th flex items have overridden alignment through the align-self property

![](https://cask.scotch.io/2015/04/flexbox-align-self.jpg)
Default value: auto

Note: The value of auto for align-self computes to the value of align-items on the element’s parent, or stretch if the element has no parent.

### Note for flex items
`float`, `clear` and `vertical-align` have no effect on a flex item, and do not take it out-of-flow.
