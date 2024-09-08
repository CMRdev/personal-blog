# CSS (cascading style sheet) 级联样式表

## 1、 选择器可以为：标签、id、类

```css
/* 复合样式选择器 */
p,
#id,
.class {
  color: green;
}
/* 让所有的选择器都有某个样式 */
* {
  font-size: 14px;
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

## 2、引入外部样式表

- 链接式(head)：`<link type="text/css" href="路径" rel=“stylesheet”>`
- 导入式：`<style type=”text/css”>@import url(“路径”) </style>`

## 3、如何使 div 进行左右布局

```css
/* 如果不添加浮动，div元素会独占一行 */
.container-left {
  width: calc(50% - 35px);
  height: auto;
  float: left;
}
```

## 4、一些知识点

- mp `Media Platform` `微信公众平台/媒体平台`

- `background-size:cover;` 此时会保持图像的纵横比并将图像缩放成将完全覆盖背景定位区域的最小大小

```css
/* 会扩大外布局 */
box-sizing: content-box;
/* 外边框不会变化 */
box-sizing: border-box;
```
