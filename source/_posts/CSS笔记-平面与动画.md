---
title: CSS笔记-平面与动画
author: yikafu
date: 2022-08-07 14:41:02
updated: 2022-08-09 20:39:22
tags: css
categories: 前端
cover: https://cdn.jsdelivr.net/gh/yikafu/blog_img/random_cover/cover7.jpg
---



# 一、CSS3-2D属性

## 1.1、transition过渡

`transition`可以制作过渡动画，常和`:hover`搭配

```css
transition: 要过渡的属性 花费时间 运动曲线 何时开始
```

1. **要过渡的属性**：如果想要所有的属性都变化过渡，写一个all就可以。
2. **花费时间**：单位是秒(必须写单位) 
3. **运动曲线**：默认是ease(可以省略)
4. **何时开始**：单位是秒(必须写单位)，可以设置延迟触发事件，默认是0s(可以省略)

## 1.2、transform的2D转换

`转换(transform)`可以实现元素的位移，旋转，缩放等效果

<img src="https://cdn.jsdelivr.net/gh/yikafu/blog_img/xy-1.png" style="zoom: 50%;" />

1. **移动translate**

   2D移动是2D转换里面的一种功能，可以改变元素在页面中的位置，**类似**定位。

    ```css
    transform:translate(x,y); 
    /*或者分开写*/
    transform:translateX(n);
    transform:translateY(n);
   
    /*如果只移动X轴*/
    transform:translate(100px,0);
    translateX(100px);
    ```

    - translate 中的百分比单位是**相对于自身元素**的

2. **旋转rotate**

   默认旋转的中心点是元素的中心点

   ```css
   transform: rotate(度数)
   /*度数单位是deg*/
   ```

  - 旋转中心点

    ```css
    transform-origin: x y;
    ```

    - x y **默认**转换的中心点是元素的中心点(50% 50%)
    - x y 设置 像素或者方位名词(top bottom left right center)

3. **缩放scale**

```css
transform: scale(x,y);
```

1. `transform:scale(1,1)`: 宽和高都放大一倍，相当于没有放大
2. `transform:scale(2,2)`：宽和高都放大了2倍
3. `transform:scale(2)`：只写一个参数，第二个参数则和第一个参数一样，相当于 `scale(2,2)`
4. `transform:scale(0.5,0.5)`：缩小
5. 可以设置转换中心点缩放，默认以中心点缩放的，而且不影响其他盒子

## 1.3、2D转换综合写法

1. 同时使用多个转换，其格式为: `transform:translate() rotate() scale()` ~~移动-旋转-缩放~~
2. 其顺序会影响转换的效果(先旋转会改变坐标轴方向)
3. **同时有位移和其他属性时候，位移要放到最前面**

# 二、动画

`animation`属性可以实现动画效果，先定义，在调用

## 2.1、keyframs定义动画

```css
@keyframes 动画名称 {
   0%{
        width:100px;
   }  
   100%{
        width:200px;
   }
}
/*-------------------------*/
@keyframes 动画名称 {
   from{
        width:100px;
   }  
   to{
        width:200px;
   }
}
```

- 0% 是动画的开始，100% 是动画的完成。这样的规则就是动画序列。
- 在 `@keyframes` 中规定某项 CSS 样式，就能创建由当前样式逐渐改为新样式的动画效果
- 动画是使元素从一种样式逐渐变化为另一种样式的效果。您可以改变任意多的样式任意多的次数。
- 用百分比来规定变化发生的时间，或用关键词 “from” 和 “to”，等同于 0% 和 100%。

## 2.2、使用动画

```css
div {
     /* 调用动画 */
     animation-name: 动画名称;
     /* 持续时间 */
     animation-duration: 持续时间;
}
```

## 2.3、动画常用属性

| **属性**                  | **描述**                                                     |
| ------------------------- | ------------------------------------------------------------ |
| @keyframes                | 规定动画。                                                   |
| animation                 | 所有动画属性的简写属性，除了animation-play-state属性。       |
| animation-name            | 规定@keyframes动画的名称。（**必须的**）                     |
| animation-duration        | 规定动画完成一个周期所花费的秒或毫秒，默认是0。（**必须的**） |
| animation-timing-function | 规定动画的速度曲线，默认是“ease”。                           |
| animation-delay           | 规定动画何时开始，默认是0。                                  |
| animation-iteration-count | 规定动画被播放的次数，默认是1，还有infinite                  |
| animation-direction       | 规定动画是否在下一周期逆向播放，默认是“normal“,alternate逆播放 |
| animation-play-state      | 规定动画是否正在运行或暂停。默认是"running",还有"paused"。   |
| animation-fill-mode       | 规定动画结束后状态，保持forwards回到起始backwards            |

- 动画的简写属性
  
    `animation：动画名称 持续时间 运动曲线 何时开始 播放次数 是否反方向 动画起始或者结束的状态`
    
    - 简写属性里面不包含 `animation-play-state`
    - 暂停动画：`animation-play-state: puased;` 经常和鼠标经过等其他配合使用
    - l想要动画走回来 ，而不是直接跳回来：`animation-direction: alternate;`
    - 盒子动画结束后，停在结束位置： `animation-fill-mode : forwards;`

# 三、 3D转换

<img src="https://cdn.jsdelivr.net/gh/yikafu/blog_img/3d_xyz.png" style="zoom:50%;" />

## 3.1、translate3d

- 3D移动在2D移动的基础上多加了一个可以移动的方向，就是z轴方向，各方位其余均与2D相同

- `translateZ`引起的变化需要搭配透视来使用

```css
/*综合写法*/
transform: translate3d(2px , 3px ,4px);
```

**透视写在被观察元素的父盒子上面**

```css
body{
    perspective: 300px;
}
```

有了透视就能看到`translateZ`引起的变化

## 3.2、3D旋转rotate3d

3D旋转：3D旋转指可以让元素在三维平面内沿着 x轴，y轴，z轴或者自定义轴进行旋转。

- `transform: rotateX(45deg)` ：沿着X轴正方向旋转45度
- `transform: rotateY(45deg)` ：沿着Y轴正方向旋转45度
- t`ransform: rotateZ(45deg)` ：沿着Z轴正方向旋转45度
- `transform: rotate3d(x,y,z,deg)` ：沿着自定义轴旋转 deg为角度(了解即可)

xyz是表示旋转轴的矢量，是标示你是否希望沿着该轴旋转，最后一个标示旋转的角度。

```css
/*沿着X轴旋转45deg*/
transform: rotate3d(1,0,0,45deg) 
/*沿着对角线旋转45deg*/
transform: rotate3d(1,1,0,45deg) 
```

### 左手准则

- 左手的手拇指指向 x / y轴的正方向，其余手指的弯曲方向就是该元素沿着x / y轴旋转的方向（正值）

## 3.3、3D呈现transform-style

1. 控制子元素是否开启三维立体环境
2. `transform-style: flat` 子元素不开启3d立体空间 (默认的)
3. `transform-style: preserve-3d` 子元素开启立体空间
4. **代码写给父级**，但是影响的是子盒子

[「transform-style和perspective属性的使用！」](https://blog.csdn.net/gjwlyxs/article/details/105463519)
