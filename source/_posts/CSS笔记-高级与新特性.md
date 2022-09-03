---
title: CSS笔记-高级与新特性
author: yikafu
date: 2022-08-01 14:39:10
updated: 2022-08-05 16:40:11
tags: css
categories: 前端
cover: https://cdn.jsdelivr.net/gh/yikafu/blog_img/random_cover/cover8.jpg
---

# 一、精灵图（sprites）

- 精灵技术主要针对于背景图片的使用，就是把多个小背景图片整合到一张大图片中
- 移动背景图片的位置使用 `background-position: x y`
- 移动的距离就是这个目标图片的x和y坐标，x右正左负，y下正上负

# 二 、CSS三角

通过将正方形分为四个三角形，将其中三个赋予透明，一个加上颜色

```css
.box1{
      width: 0;
      height: 0;
      border: 50px solid transparent;
      border-top-color: red;
        }
```

# 三、 CSS用户界面

## 3.1、 鼠标指针

```css
li {
    cursor: default ; 
}
```

## 3.2、 outline轮廓线

- 给表单添加 `outline:0`; 或者`outline: none`;样式后，就可以去掉默认的蓝色边框

```css
input {
    outline: none;
}
```

## 3.3、防止拖拽文本域

```css
textarea {
    resize: none;
}
```

# 四、vertical-align

- 用于设置**图片**或者**表单（行内块元素）**和**文字垂直对齐**。

```css
vertical-align: baseline | top | middle | bottom
```

| 值       | 描述                           |
| -------- | ------------------------------ |
| baseline | 默认，元素放置在父元素的基线上 |
| top      | 顶线对齐                       |
| middle   | 中线对齐                       |
| bottom   | 底线对齐                       |

![](https://cdn.jsdelivr.net/gh/yikafu/blog_img/vertical_img1.jpg)

- 图片底侧会有一个空白缝隙，原因是行内块元素会和文字默认基线对齐
  - 给图片添加 `vertical-align : middle/top/bottom` 等
  - 把图片转换为块级元素 `display:block;`

# 五、溢出文字显示

## 5.1、单行文本溢出省略号显示

```css
/* 1.先强制一行内显示文本 */
white-space: nowrap;
/*默认 normal 是自动换行，nowrap是强制一行显示文本*/

/* 2.超出的部分隐藏 */
overflow: hidden;

/* 3.文字用省略号替代超出的部分*/
text-overflow: ellipsis;
/*ellipsis:省略号*/
```

## 5.2、多行文本溢出显示省略号显示（了解）

```css
overflow: hidden;
text-overflow: ellipsis;
/* 弹性伸缩盒子模型显示 */
display: -webkit-box;
/* 限制在一个块元素显示的文本的行数 */
-webkit-line-clamp: 2;
/* 设置或检索伸缩盒对象的子元素的排列方式 */
-webkit-box-orient : vertical;
```

- 有较大的兼容性问题，更推荐让后台人员来做这个效果

# 六、常见布局技巧

## 6.1、margin负值的运用

实现多个边框图相连，实现共用一条边

1. 两个盒子加边框1px，浮动（~~贴紧会出现边框叠加~~）
2. 给右边盒子添加`margin-left: -1px`
3. 鼠标经过某个盒子的时候，提高当前盒子的层级即可
  - 如果没有定位，则加相对定位(保留位置)
  - 如果有定位，则加 `z-index`

![](https://cdn.jsdelivr.net/gh/yikafu/blog_img/mar_fu_gif1.gif)

## 6.2、文字围绕浮动元素

浮动元素不会压住文字，自动围绕

## 6.3、行内块巧妙运用

页码在页面中间显示：

1. 把这些链接盒子转换为行内块，之后给父级指定 `text-align: center`
2. 利用行内块元素中间有缝隙，并且给父级添加 `text-align: center` ，行内块元素会水平居中

#  七、HTML5新特性

## 7.1、HTML5新增语义标签

- `<header>`头部标签
- `<nav>`导航标签
- `<article>`内容标签
- `<section>`定义文档某个区域
- `<aside>`侧边栏标签
- `<footer>`尾部标签

## 7.2、HTML5新增媒体标签

- `<video>`插入视频标签尽量使用mp4格式

  ```html
  <video src="视频地址"></video>
  ```

  | 属性          | 描述                 |
  | ------------- | -------------------- |
  | autoplay      | 视频加载完成自动播放 |
  | controls      |向用户具示播放控件   |
  | width、height  | 宽、高 |
  | loop | 是否循环播放 |
  | preload | 是否预加载视频（有了autoplay则忽略） |
  | poster | 加载画面图片 |
  | muted | 静音播放 |

- `<audio>`插入音频

    ```html
    <audio src="音频地址"></audio>
    ```

    只有`autoplay` 、 `controls` 、 `loop` 三个属性，同上

## 7.3、HTML5新增input类型与属性

1. 新增类型：color、date、datetime、email、month、number、tel（手机号码）、time、url、week等
  - 用于限制`input`的输入类型

    ```html
    <input type="color" />
    ```

2. 新增属性：autofocus、require 、placeholder、autocomplete 、multiple等

    | 属性         | 描述                                                         |
    | ------------ | ------------------------------------------------------------ |
    | autofocus    | 自动聚焦属性，页面加载亮成自动聚焦到指定表单                 |
    | require      | 内容不能为空，必填                                           |
    | placeholder  | 表单的提示信息，存在默认值将不显示                           |
    | autocomplete | 当用户在字段开始健入时，浏览器甚于之前键入过的值，应该显示出在字段中填写的选项。默认值为"on",需要放在表单内，同时加上name属性，同时成功提交 |
    | multiple     | 可以多选文件提交                                             |

    可以使用`input::placeholder {  color="red" ;}`设置提示信息的字体颜色

# 八、CSS3新特性

## 8.1、属性选择器

| 选择符        | 简介                                  |
| ------------- | ------------------------------------- |
| E[att]        | 选择具有att属性的E元素                |
| E[att=“val”]  | 选择具有att属性且属性值等于val的E元素 |
| E[att^=“val”] | 匹配具有att属性且值以val开头的E元素   |
| E[att$=“val”] | 匹配具有att属性且值以val结尾的E元素   |
| E[att*=“val”] | 匹配具有att属性且值中含有val的E元素   |

## 8.2、结构伪类选择器

- 根据父级选择器选择里面的子元素

| 选择符             | 简介                        |
| ------------------ | --------------------------- |
| E:first-child      | 匹配父元素中的第一个子元素E |
| E:last-child       | 匹配父元素中最后一个E元素   |
| E:nth-child(n)     | 匹配父元素中的第n个子元素E  |
| E:first-of-type    | 指定类型E的第一个           |
| E:last-of-type     | 指定类型E的最后一个         |
| E:nth-of-type（n） | 指定类型E的第n个            |

- ### nth-child(n)

  - n可以是**数字，关键字和公式**

  1. n如果是数字，就是选择第n个子元素，里面数字从1开始
  2. n可以是关键字：**even** 偶数，**odd**奇数
  3. n可以是公式：常见的公式如下（如果n是公式，则从0开始计算，但是第0个元素或者超出了元素的个数会被忽略）

  | 公式 | 取值                            |
  | ---- | ------------------------------- |
  | 2n   | 偶数（等价于even）              |
  | 2n+1 | 奇数（等价于odd）               |
  | 5n   | 5 10 15 …（5的倍数）            |
  | n+5  | 从第5个开始（包含第五个）到最后 |
  | -n+5 | 前5个（包含第5个）              |

- `nth-child(n)` 和 `nth-of-type(n)`的区别
  
  1. **`nth-child` 对父元素里面所有孩子排序选择(序号是固定的)，先找到第n个孩子，然后看看是否和E匹配**
  2. **`nth-of-type` 对父元素里面指定子元素进行排序选择，先去匹配E,然后再根据E 找第n个孩子**

## 8.3、伪元素选择器

- 利用CSS**创建新标签元素**，而不需要HTML标签

| 选择符   | 简介                     |
| -------- | ------------------------ |
| ::before | 在元素内部的前面插入内容 |
| ::after  | 在元素内部的后面插入内容 |

```css
元素名::before {
    
}
```

- before 和 after 必须有 **content** 属性

## 8.4、CSS3盒子box-sizing

- CSS3 中可以通过`box-sizing` 来指定盒模型
  
- 第一种情况是 CSS 的盒子模型，盒子大小为 width + padding + border
- 此种情况盒子大小为 宽度 + 内边距 + 边框，这也是我们之前写盒子所默认的
  ```css
  box-sizing: content-box;
  ```

- 第二种情况是 CSS3 的盒子模型，盒子大小为 width
- 此种情况盒子大小为 宽度，不包括内边距和边框，这样 padding 和 border 就不会撑大盒子了(前提是 padding 和 border 不会超过 width 宽度)
  ```css
  box-sizing: border-box;
  ```
  ```css
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    /*  这样的话padding和border就不会撑大盒子了 */
  }
  ```

## 8.5、CSS3其他特性

1. filter函数

    ```css
      filter: 函数();
    ```

    ```css
      /*高斯模糊处理*/
      filter: blur(xxx px)
      /*数值越大，模糊越厉害*/
    ```

2. calc函数

- `calc()` 此CSS函数让你在声明CSS属性值时执行一些计算

    ```css
      /*计算盒子宽度 */
      width:calc(100% - 10px); 
    ```

    括号里面可以使用 + - * / 来进行计算
