---
title: Bootstrap
layout: post
tags: 前端
categories: ''
---

2020-10-26 今天正式进行bootstrap学习

## 1. 布局

响应式布局：通过父元素作为布局容器，来配合子元素来实现变化效果。

Containers，通过**. container**进行布局。**.row** 控制行，**.col** 控制列。

.col-* 其中的*为所占比例；总大小规定为12，.col-4代表占 4/12。

![image-20201026150405376](C:\Users\zheng\AppData\Roaming\Typora\typora-user-images\image-20201026150405376.png)

```javascript
<div class="container">
  <div class="row">
    <div class="col">col</div>
    <div class="col">col</div>
    <div class="col">col</div>
    <div class="col">col</div>
  </div>
  <div class="row">
    <div class="col-8">col-8</div>
    <div class="col-4">col-4</div>
  </div>
</div>
```

具体参考：https://v4.bootcss.com/docs/layout/grid/

Bootstrap开发四部曲：

```
1.创建文件夹结构、

2.创建html骨架结构

3.引入相关样式文件

4.书写内容
```



## 2.栅格系统

bootstarp栅格系统很强大！

.container 和 .container-fluid（流式布局 100%占比）

```
twelve column system, five default responsive tiers, Sass variables and mixins, and dozens of predefined classes.
12列系统，5个默认响应层，Sass变量和混合以及数十个预定义类
```

```html
<div class="container">
  <div class="row row-cols-2">
    <div class="col">Column</div>
    <div class="col">Column</div>
    <div class="col">Column</div>
    <div class="col">Column</div>
  </div>
</div>
```

row 代表行，row-cols-2代表每行两列；效果如下：

![image-20201026161013823](C:\Users\zheng\AppData\Roaming\Typora\typora-user-images\image-20201026161013823.png)

------

1. 如果一个container中，占比小于12，则出现空缺现象； 如果大于12，将出现新建一行的现象。

2. 提供多类名写法，class=“col-lg-3  col-md-4 col-sm-6 col-xs-12”，即大屏幕下占3份，中等屏幕占4份，小屏幕占6份，超小屏幕占12个。

3. 列嵌套最好加一个行，这样可以消除父元素的padding值。

4. 盒子偏移；

   ```html
   <div>
       <div class = "row">
           <div class= "col-md-4">左侧盒子</div>
           <div class= "col-md-4 col-md-offset-4">右侧盒子</div>
       </div> 
   </div>
   ```

   ![](C:\Users\zheng\AppData\Roaming\Typora\typora-user-images\image-20201027101025412.png)

5. 列排序：左右推拉

   ```html
   <div class= "row">
       <div class="col-lg-4 col-lg-push-8">
           左侧盒子
       </div>    
       <div class="col-lg-4 col-lg-pull-4">
           右侧盒子
       </div>    
   </div>
   ```

6. 响应式工具【大屏显示，小屏显示等】

   ![image-20201027104112000](C:\Users\zheng\AppData\Roaming\Typora\typora-user-images\image-20201027104112000.png)

   在某个屏幕下隐藏

   ```html
   <div class = ".comtainer">
   	<div class = "row"></div>
       <div class = "col-xs-3 ">
           <span class=" visible-lg"> 只有在大屏幕才显示</span>
       </div>
       <div class = "col-xs-3">2</div>
   	<div class = "col-xs-3 hidden-xs">在超小屏幕隐藏</div>
       <div class = "col-xs-3">4</div>
   </div>
   ```

   