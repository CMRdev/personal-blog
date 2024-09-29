# CSS (cascading style sheet) 级联样式表

## 1、引入外部样式表

- 链接式(head)：`<link type="text/css" href="路径" rel=“stylesheet”>`
- 导入式：`<style type=”text/css”>@import url(“路径”) </style>`

## 2、em 和 rem 的区别

- rem（font size of the root element）是指相对于`根元素`的字体大小的单位

- em（font size of the element）是指相对于`父元素`的字体大小的单位，如当前对行内文本的字体尺寸未被人为设置，则相对于`浏览器的默认字体尺寸16px`

## 3、box-sizing

- `box-sizing`：定义了浏览器应该如何计算一个元素的`总宽度`和`总高度`

  - CSS 盒子模型组成：`content、padding、border、margin`
  - 当你对一个元素设置`width、height`时，只会应用到这个元素的内容区`content`，绘制到屏幕上时，盒子的宽高会加上`边框`和`内边距`值
  - `content-box`：默认值，元素被设置的宽高只作用于`content`
  - `border-box`：元素的`边框和内边距`的值是包含在元素的`width(height)`内的，这使我们更容易地设定一个元素地宽高

## 3、一些知识点

- `background-size:cover;` 此时会 **保持图像的纵横比** 并将图像缩放成将完全覆盖背景定位区域的最小大小

- 选择器可以为：`标签、id、类`

  ```css
  /* 让所有的选择器都有某个样式 */
  * {
    font-size: 14px;
  }
  /* 复合样式选择器 */
  p,
  #id,
  .class {
    color: green;
  }
  /* 交集选择器：标签+类、标签+id */
  h3.second {
    color: green;
  }
  /* 后代选择器：p段落里的a标签，中间用空格隔开 */
  p a {
    color: green;
  }
  ```

- 如何使 div 进行左右布局

  ```css
  /* 如果不添加浮动，div元素会独占一行 */
  .container-left {
    width: calc(50% - 35px);
    height: auto;
    float: left;
  }
  ```
