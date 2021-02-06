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

   

## 3.组件

#### 1.下拉菜单

```html
<div class="dropdown">
  <button class="btn btn-secondary dropdown-toggle" type="button" id="dropdownMenuButton" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
    Dropdown button
  </button>
  <div class="dropdown-menu" aria-labelledby="dropdownMenuButton">
    <a class="dropdown-item" href="#">Action</a>
    <a class="dropdown-item" href="#">Another action</a>
    <a class="dropdown-item" href="#">Something else here</a>
  </div>
</div>
```

1.设置class 为dropdown

2.为dropdown写一个菜单dropdown-menu

3.给菜单加一个button，一定要定义  data-toggle="dropdown"  就ok了

注意：aria-haspopup，aria-expanded没啥鸟用，给语音设备等设备用的，可以不写

#### 2.按钮组

```html
<div class="btn-group" role="group" aria-label="Basic example">
  <button type="button" class="btn btn-secondary">Left</button>
  <button type="button" class="btn btn-secondary">Middle</button>
  <button type="button" class="btn btn-secondary">Right</button>
</div>
```

写一个btn-group将按钮包含起来就行了

#### 3.按钮工具栏

```html
<div class="btn-toolbar" role="toolbar" aria-label="Toolbar with button groups">
  <div class="btn-group mr-2" role="group" aria-label="First group">
    <button type="button" class="btn btn-secondary">1</button>
    <button type="button" class="btn btn-secondary">2</button>
    <button type="button" class="btn btn-secondary">3</button>
    <button type="button" class="btn btn-secondary">4</button>
  </div>
  <div class="btn-group mr-2" role="group" aria-label="Second group">
    <button type="button" class="btn btn-secondary">5</button>
    <button type="button" class="btn btn-secondary">6</button>
    <button type="button" class="btn btn-secondary">7</button>
  </div>
  <div class="btn-group" role="group" aria-label="Third group">
    <button type="button" class="btn btn-secondary">8</button>
  </div>
</div>
```

1. 设定 class="btn-toolbar" 将所有的按钮放在一块
2. 如果想让按钮垂直排列，设置 class 为 btn-group-vertical

```html
<div class="btn-group-vertical">
    ...
</div>
```

#### 4.输入组

直接上网站看案例就够了

[网站]: https://v4.bootcss.com/docs/components/input-group/

#### 5.导航条

##### 	基类 nav

```html
<nav class="navbar navbar-expand-lg navbar-light bg-light">
  <a class="navbar-brand" href="#">Navbar</a>
    <!--用来做屏幕的自适应,缩小尺寸会折叠-->
  <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
    <span class="navbar-toggler-icon"></span>
  </button>
<!--导航条中其他按钮-->
  <div class="collapse navbar-collapse" id="navbarSupportedContent">
    <ul class="navbar-nav mr-auto">
      <li class="nav-item active">
        <a class="nav-link" href="#">Home <span class="sr-only">(current)</span></a>
      </li>
      <li class="nav-item">
        <a class="nav-link" href="#">Link</a>
      </li>
      <li class="nav-item dropdown">
        <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
          Dropdown
        </a>
        <div class="dropdown-menu" aria-labelledby="navbarDropdown">
          <a class="dropdown-item" href="#">Action</a>
          <a class="dropdown-item" href="#">Another action</a>
          <div class="dropdown-divider"></div>
          <a class="dropdown-item" href="#">Something else here</a>
        </div>
      </li>
      <li class="nav-item">
        <a class="nav-link disabled" href="#" tabindex="-1" aria-disabled="true">Disabled</a>
      </li>
    </ul>
    <form class="form-inline my-2 my-lg-0">
      <input class="form-control mr-sm-2" type="search" placeholder="Search" aria-label="Search">
      <button class="btn btn-outline-success my-2 my-sm-0" type="submit">Search</button>
    </form>
  </div>
</nav>
```

##### 导航条位置

【默认导航条navbar ，固定在上方 navbar fixed-top，固定在下方navbar fixed-bottom】

```html
<nav class="navbar navbar-light bg-light">
  <a class="navbar-brand" href="#">Default</a>
</nav>
```

##### 背景色设置

```html
<nav class="navbar navbar-dark bg-dark">
  <!-- Navbar content -->
</nav>

<nav class="navbar navbar-dark bg-primary">
  <!-- Navbar content -->
</nav>

<nav class="navbar navbar-light" style="background-color: #e3f2fd;">
  <!-- Navbar content -->
</nav>
```

#### 6.分页

class="pagination"； 禁用直接使用class = "disabled"

```html
<nav aria-label="Page navigation example">
  <ul class="pagination">
    <li class="page-item"><a class="page-link" href="#">Previous</a></li>
    <li class="page-item"><a class="page-link" href="#">1</a></li>
    <li class="page-item"><a class="page-link" href="#">2</a></li>
    <li class="page-item"><a class="page-link" href="#">3</a></li>
    <li class="page-item"><a class="page-link" href="#">Next</a></li>
  </ul>
</nav>
```

#### 7.标签和徽章

标签 基类 label label-primary

```html
<span class="label label-primary"> 标签 </span>
```

徽章 基类badge

```html
<span class="badge badge-primary"> 标签 </span>
```

#### 8.巨幕

包含容器的巨幕，可以做成无轮廓

基类 jumbotron

```html
<div class="jumbotron jumbotron-fluid">
  <div class="container">
    <h1 class="display-4">Fluid jumbotron</h1>
    <p class="lead">This is a modified jumbotron that occupies the entire horizontal space of its parent.</p>
  </div>
</div>
```

#### 9.卡片

基类 card，适合做商品展示，上面放图片，下面放文字

```html
<div class="card" style="width: 18rem;">
  <img src="..." class="card-img-top" alt="...">
  <div class="card-body">
    <h5 class="card-title">Card title</h5>
    <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
    <a href="#" class="btn btn-primary">Go somewhere</a>
  </div>
</div>
```

#### 10.警告框

基类 alert ，加入可关闭的按钮 class="close" data-dismiss="alert"

```html
<div class="alert alert-warning alert-dismissible fade show" role="alert">
  <strong>Holy guacamole!</strong> You should check in on some of those fields below.
  <button type="button" class="close" data-dismiss="alert" aria-label="Close">
    <span aria-hidden="true">&times;</span>
  </button>
</div>
```

#### 11.进度条

基类 progress，相当于创建一个血槽

里层放入progress-bar，相当于血量，width控制血量

.bg-success设置颜色

.progress-bar-striped 加上条纹

.progress-bar-animated 让条纹动起来，有点秀



如果要堆叠效果，就写多个

```
<div> progress-bar<\div>
```

 在

```
<div>  progress <\div>
```

类中

```html
<div class="progress">
  <div class="progress-bar" role="progressbar  bg-success" style="width: 25%" aria-valuenow="0" aria-valuemin="0" aria-valuemax="100"></div>
</div>
```

#### 12.列表组

基类 list-group

```html
<ul class="list-group">
  <li class="list-group-item d-flex justify-content-between align-items-center">
    Cras justo odio
    <span class="badge badge-primary badge-pill">14</span>
  </li>
  <li class="list-group-item d-flex justify-content-between align-items-center">
    Dapibus ac facilisis in
    <span class="badge badge-primary badge-pill">2</span>
  </li>
  <li class="list-group-item d-flex justify-content-between align-items-center">
    Morbi leo risus
    <span class="badge badge-primary badge-pill">1</span>
  </li>
</ul>
```

### 4.插件

### 5.页面整合

作者采用的动态加载页面为：

​	1.清空基础文件中的相关模块 empty()

​	2.保留新加载的文件保留主体内容

​	3.动态加载链接 load(url)到特定区域

### 6.jqgrid插件

1. jqgrid都是以ajax方式进行值的传递，所以格式也是ajax格式

