<!--
 * @Author: shenxh
 * @Date: 2021-12-13 17:07:40
 * @LastEditors: shenxh
 * @LastEditTime: 2021-12-15 15:51:39
 * @Description: CSS 背景
-->

- [背景色](#背景色)
- [背景图像](#背景图像)
- [背景图像尺寸](#背景图像尺寸)
- [重复图像](#重复图像)
- [固定图像](#固定图像)
- [图像起始位置](#图像起始位置)
- [属性简写 (建议)](#属性简写-建议)

# 背景色
`background-color` 属性定义了元素的背景颜色
```
body {
    background-color: #fff;
}
```
CSS 中，颜色值通常以以下方式定义:
+ 十六进制 - 如: `#ff0000`, 可简写为: `#f00`
+ RGB - 如: `rgb(255, 0, 0)`
+ 颜色名称 - 如: `red`

# 背景图像
`background-image` 属性描述了元素的背景图像

默认情况下，背景图像进行**平铺重复**显示，以覆盖整个元素实体
```
body {
    background-image: url('myBackground.png');
}
```

# 背景图像尺寸
我们可以通过 `background-size` 来设置背景图尺寸

比如
```
body {
    background-size: 100% 100%; /* 将计算相对于背景定位区域的百分比。第一个值设置宽度，第二个值设置的高度。如果只给出一个值，第二个是设置为 auto(自动) */
    background-size: 200px 100px; /* 设置背景图片高度和宽度。第一个值设置宽度，第二个值设置的高度。如果只给出一个值，第二个是设置为 auto(自动) */
    background-size: contain; /* 时会保持图像的纵横比并将图像缩放成将适合背景定位区域的最大大小 */
    background-size: cover; /* 此时会保持图像的纵横比并将图像缩放成将完全覆盖背景定位区域的最小大小 */
}
```

# 重复图像
默认情况下，重复 `background-image` 的垂直和水平方向

我们可以使用 `background-repeat` 来设置是否及如何重复
```
body {
    background-repeat: repeat; /* [默认]背景图像将向垂直和水平方向重复 */
    background-repeat: repeat-x; /* 只有水平位置会重复背景图像 */
    background-repeat: repeat-y; /* 只有垂直位置会重复背景图像 */
    background-repeat: no-repeat; /* 不重复 */
    background-repeat: inherit; /* 继承父元素 */
}
```

# 固定图像
默认情况下, 背景图片随着页面的滚动而滚动

我们可以使用 `background-attachment` 来设置是否固定或者随着页面的其余部分滚动
```
body {
    background-attachment: scroll; /* [默认]背景图片随着页面的滚动而滚动 */
    background-attachment: fixed; /* 背景图片不会随着页面的滚动而滚动 */
    background-attachment: local; /* 背景图片会随着元素内容的滚动而滚动 */
    background-attachment: initial; /* 设置该属性的默认值 */
    background-attachment: inherit; /* 继承父元素 */
}
```

# 图像起始位置
`background-position`
|属性值|描述|
|-|-|
|`left top`<br />`left center`<br />`left bottom`<br />`right top`<br />`right center`<br />`right bottom`<br />`center top`<br />`center center`<br />`center bottom`|如果仅指定一个关键字，其他值将会是 `center`|
|x% y%|第一个值是水平位置，第二个值是垂直位置<br />左上角是 `0% 0%`。右下角是 `100% 100%`<br />如果仅指定了一个值，其他值将是 `50%`<br />默认值为：`0% 0%`|
|xPos yPos|第一个值是水平位置，第二个值是垂直位置<br />左上角是 `0`<br />单位可以是像素 `0px 0px` 或任何其他 CSS单位<br />如果仅指定了一个值，其他值将是 `50%`<br />你可以混合使用 `%` 和 `positions`|
|inherit|继承父元素|

# 属性简写 (建议)
举例:
```
body {
    background-color: #fff; /* 背景色 */
    background-image: url('myImg.png'); /* 背景图 */
    background-repeat: no-repeat; /* 不重复 */
    background-position: 0 0; /* 起始位置: x-0 y-0 */
}
```
上面例子可以这样写:
```
body {
    background: #fff url('myImg.png') no-repeat 0 0;
}
```

当使用简写属性时，属性值的顺序为:
+ background-color
+ background-image
+ background-repeat
+ background-attachment
+ background-position

以上属性无需全部使用，你可以按照页面的实际需求来选择使用
