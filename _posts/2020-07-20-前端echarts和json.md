---
title: echarts和json格式
layout: post
tags: 前端
categories: ''
---

# 一、JSON格式文件解析

1.JSON是什么

JavaScript Object Notation，即JavaScript 对象标记法；参考了JavaScript对象语法规则;

JSON格式永不升级【giao】

2.JSON语法规则

- 数组用方括号 [ ]

- 对象用大括号{ }

- 名称/值対（name/value)组合成数组和对象

- 名称置于双引号中，值有字符串，数值，布尔值，null，对象和数组

- 并列的数据之间用逗号“ , ”分隔

  ```json
  {
  "name" :  "liudehua"
  "age": "28"
  }
  ```

3.JSON和XML

JSON与XML优势

- 没有结束标签

- 能够直接被JavaScript解析

- 可以直接使用数组

  JSON格式

  ```json
  {
  "name" :  "liudehua"
  "age": "28"
  "friends":["Lily","Lucy","Gwen"]
  }
  ```

  XML格式

  ```xml
  <root>
  	<name>Liudehua</name>
      <age>26</age>
      <friends>Lily</friends>
      <friends>Lucy</friends>
      <friends>Gwen</friends>
  </root>
  
  ```

JSON解析和生成



# 二、echars实现动态图表

https://www.bilibili.com/video/BV17t4y1175V

* 拖拽重计算
* 数据视图 查看源数据
* 动态类型切换【折现，柱形等多种形式一键转换】
* 值域漫游
* 数据区域缩放【区间筛选】
* 多图联动
* 百搭时间轴【时间轴，变化趋势】
* 大规模散点【百万级数据展现】
* 力导向布局
* 动态数据添加
* 多维度图例开关
* 商业BL
* 图表混搭【图表中搭配图表】
* 特效

### 2.1介绍

底层采用zrender，开源免费，功能丰富、社区活跃的JavaScript库。

数据格式

1. 支持key-value
2. 二维表
3. TypedArray

流数据的支持

1. 流数据的动态渲染
2. 增量渲染技术

### 2.2快速入门

1. 引入echarts.js文件

   ```html
   <script src="echarts.min.js"></script>
   ```

   

2. 准备呈现图表的盒子

   ```html
   <div style="width:600px;height:600px"></div>
   ```

   

3. 初始化echarts实例对象

   ```html
   <script>
   var mecharts = echarts.init(document.querySelector('div'))
   </script>
   ```

4. 准备配置项

   ```javascript
   option = {
       xAxis: {
           type: 'category',
           data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
       },
       yAxis: {
           type: 'value'
       },
       series: [{
           data: [150, 230, 224, 218, 135, 147, 260],
           type: 'line'
       }]
   };
   ```

5. 将配置项设置给你实例对象

   ```javascript
   mecharts.setOption(option)
   ```

### 2.3配置项

```html
<script>
option = {
    xAxis: {
        type: 'category', //类目轴
        data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
    },
    yAxis: {
        type: 'value' //数值轴
    },
    series: [{			//系列列表
        data: [150, 230, 224, 218, 135, 147, 260],
        type: 'line'  
    }]
};
</script>

```

配置项较多，使用时直接查阅官方文档 https://echarts.apache.org/zh/option.html#title

### 2.4echarts常用图表

7大图表

柱状图、折线图、散点图、饼图、地图、雷达图、仪表盘图

#### 1.常见效果

标记：最大值、最小值、平均值

x,y轴切换，只需要改变xAxis,yAxis

markPoint，markLine

label




```html
<script>
    var myechart = echarts.init(document.getElementById("myechart"));
    option = {
        title: {
            text: "Main Title",
            subtext: "Sub Title",
            left: "center",
            top: "top",
            textStyle: {
                fontSize: 30
            },
            subtextStyle: {
                fontSize: 20
            }
        },
        xAxis: {
            type: 'category',
            data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
        },
        yAxis: {
            type: 'value'
        },
        series: [{
            data: [150, 230, 224, 218, 135, 147, 260],
            type: 'bar',
            label: {
                show: true, //显示柱状图数值
                color: 'white',
                rotate:30,
            },
            markLine: {
                data: [{
                    0: {},
                    type: "average"
                }]//设置平均值线
            },
            markPoint: {
                data: [{
                    type: "max",
                    name: '最大值'
                },//设置最大值
                {
                    type: "min",
                    name: '最小值'
                } //设置最小值

                ],
                symbol: "pin"
            },

            barWidth: '30%', //设置柱的宽度
        },
        
    ],
    };
    myechart.setOption(option)
</script>
```
#### 2.通用配置title

1. 文字样式 textStyle
2. 标题边框 borderWidth，borderColor，borderRadius
3. 标题位置left ，top，right，bottom

#### 3.通用配置tooltip

提示框组件，用于配置鼠标滑过或者点击图表时候的显示

1. 触发类型：trigger

   ```javascript
   trigger:"item"
   trigger:"axis"
   ```

   item显示name和数值；axis指只要移入柱子的轴里面就触发name和数值。

2. 触发时机：triggerOn

   mouserover，click

   ```javascript
   triggerOn:"mouseover"
   triggerOn:"click"
   ```

3. 格式化：formatter

   决定鼠标触发后显示的内容，支持字符串和函数。

   格式化字符串：

   ```javascript
   formatter:"{b}的成绩是{c}"
   ```

   函数：

   ```javascript
   formatter：function(arg){
   return a[0].name+'的分数是'+arg[0].data}
   ```

   

#### 4.通用配置toolbox

导出图片、数据视图、动态类型切换、数据区域缩放、重置

```javascript
toolbox{
feature:{
saveAsImage:{},//导出图片
dataView:{},//数据视图
restore:{},//重置视图
dataZoom:{},//区域缩放
magicType:{
    type:['bar','line']
} // 柱状图折线图切换，即动态图表切换
}
}
```

#### 5.通用配置legend

legend图例，用于对系列进行筛选，结合series使用，元素来自series中的name名字

```
legend:{['语文'，数学]}
```

### 2.5折线图

#### 1.常见效果

1. 最大值最小值平均值 markPoint，markLine

2. 标注区间markArea

3. 平滑 smooth 

4. 线性lineStyle -> 颜色：color,线型【实线，虚线】type：dash/solid

5. 填充风格【面积填充】 areaStyle，对折线以下的面积进行填充

6. 设置x轴的起点， boundaryGap:false,从第一个元素开始，与坐标轴没有间隔

7. 缩放，控制y轴是否从0开始；scale:true可以脱离0值

8. 折线堆叠效果stack，stack后面的字符串可以是任意字符，只要相同，就可以叠加；

   tip：使用areaStyle效果更好

```html
<script>
      var myechart = echarts.init(document.getElementById("myechart"));
    option = {
    xAxis: {
        type: 'category',
        data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'],
        boundaryGap:false
    },
    yAxis: {
        type: 'value'，
        scale:true
    },
    },
    series: [{
        data: [150, 230, 224, 218, 135, 147, 260],
        type: 'line',
        markPoint:{
            data:[{
                type: "max"
            },
            {
                type: "min"
            }]
        },
        markLine:{
            data:[{
                type:"average",

            }]
        },
        markArea:{
            data:[
            [{xAxis:'Mon'},{xAxis:'Wed'}],
            [{xAxis:'Fri'},{xAxis:'Sat'}]   
            ]},
        smooth:true,
        lineStyle:{ color:"green",
                     type:"dash"},
        areaStyle:{ color:"blue"}
    }]
};
    myechart.setOption(option)
</script>
```

堆叠效果

```html
<script>
    var myechart = echarts.init(document.getElementById("myechart"));
    option = {
        xAxis: {
        type: 'category',
        boundaryGap: false,
        data: ['周一', '周二', '周三', '周四', '周五', '周六', '周日']
    },
    yAxis: {
        type: 'value'
    },
    series: [
        {
            name: '邮件营销',
            type: 'line',
            stack: '总量',
            data: [120, 132, 101, 134, 90, 230, 210],
            areaStyle:{}
        },
        {
            name: '联盟广告',
            type: 'line',
            stack: '总量',
            data: [220, 182, 191, 234, 290, 330, 310],
            areaStyle:{}
        },
       
    ]
};
        myechart.setOption(option)
</script>
```

#### 2.折线图特点

折线图通常用来表示时域区域内的展示

### 2.6散点图

#### 1.常见效果

1. x轴和y周的数据是一个二维数组；
2. xAxis和yAxis中的type设置为value
3. **气泡图效果**：散点大小不同 symbolSize；散点颜色不同 itemStyle.color
4. **涟漪动画效果**： type：effectScatter  【即将scatter改成effectScatter】
5. 可以通过rippleEffect中scale来控制；效果可以使用showEffectOn:render或者emphasis来确定

```html
<script>
    var myechart = echarts.init(document.getElementById("myechart"));
    var data = [
            [118, 85],
            [145, 51],
            [144, 46],
            [147, 78],
            [155, 69],
            [121, 83],
            [125, 60],
            [113, 56],
            [163, 62],
            [111, 84],
            [139, 58],
            [159, 81],
            [159, 62],
            [181, 83],
            [182, 65],
            [153, 48],
            [182, 51],
            [144, 53],
            [135, 42],
            [127, 74],
            [119, 85],
            [161, 64],
            [133, 66],
            [141, 88],
            [180, 54],
            [181, 75],
            [127, 43],
            [128, 78],
            [158, 47],
            [153, 79],
            [172, 62],
            [115, 42],
            [150, 67],
            [180, 75],
            [171, 46],
            [132, 63],
            [116, 45],
            [145, 69],
            [126, 57],
            [188, 46],
            [176, 88],
            [112, 52],
            [112, 90],
            [188, 77],
            [114, 80],
            [157, 82],
            [146, 73],
            [167, 46],
            [122, 82]
        ],
        option = {
            xAxis: {
                type: 'value',
                scale: true
            },
            yAxis: {
                type: 'value',
                scale: true
            },
            series: [{
                name: '1990',
                data: data,
                type: 'scatter',
                type:'effectScatter',// 开启涟漪动画
                rippleEffect:{scale:3},
                showEffectOn:'emphasis',//renders是默认效果
                
                scale: true,
                symbolSize: function (arg) {
                    // console.log(arg)
                    let height = arg[0] / 100
                    let weight = arg[1]
                    let bmi = weight / (height * height)
                    if (bmi > 28) {
                        return 20
                    }
                    return 10
                },
                itemStyle: { //颜色更改也可以使用函数
                    color: function (arg) {
                        console.log(arg)
                        let height = arg.data[0] / 100
                        let weight = arg.data[1]
                        let bmi = weight / (height * height)
                        if (bmi > 28) {
                            return 'red'
                        }
                        return 'green'
                    },
                }
            }]
        }

    myechart.setOption(option)
</script>
```

#### 2.散点图特点

1. 散点图可以帮助我们推断出不同维度数据之间的相关性
2. 散点图经常结合地图进行标注

### 2.7小结1--直角坐标系常用配置

直角坐标系图表：直方图、折线图、散点图

#### 1. 配置1 grid

grid是用来控制直角坐标系的布局和大小

x轴和y轴就是在grid的基础上进行绘制的

1. 显示grid --- show
2. grid的表框--- borderWidth、borderColor
3. grid的位置和大小 --- left、top、right、bottom、width、height

```javascript
    option = {
        grid:{
            show:true, //上下左右有边框
            borderWidth:10,//边框宽度
            borderColor:'red',//边框颜色
            left:200,//边框发生了移动
        },
        ...
        }
```

#### 2. 配置2 坐标轴axis

坐标轴分为x轴和y轴

一个grid中最多有两种位置的x轴和y轴

- 坐标轴类型type

  value：数值轴，自动会从目标数据中读取数据

  category：**类目轴，该类型必须通过data设置类目数据**

- 显示位置position

  xAxis:可取值为top或者bottom

  yAxis：可取值为left或者right

#### 3. 配置3 区域缩放dataZoom

dataZoom用于区域缩放，对数据范围过滤，x轴y轴都可以使用

dataZoom是一个数组，意味着可以配置多个区域缩放器

- 类型 type

  slider：滑块

  inside：内置，依靠鼠标滚轮或者双指缩放

- 指明产生作用的轴

  xAxisIndex，yAxisIndex，一般写0即可

  ```javascript
      option = {
          grid:{
              show:true, //上下左右有边框
              borderWidth:10,//边框宽度
              borderColor:'red',//边框颜色
              left:200,//边框发生了移动
          },
          dataZoom:[{
              type:'slider',//滑块
              xAxisIndex:0, //0代表第0个x轴，如果两个的话，可以指定1
          },
          {
              type:'slider',//
              yAxisIndex:0,//0代表第0个y轴，如果两个的话，可以指定1
          },
      ],
      ...
      }
  ```



### 2.8饼图

#### 1.通用设置

数据结构

```javascript
var piedata= [
                {value: 1048, name: '搜索引擎'},
                {value: 735, name: '直接访问'},
                {value: 580, name: '邮件营销'},
                {value: 484, name: '联盟广告'},
                {value: 300, name: '视频广告'}
            ],
```

```javascript
    option = {
        series:[{
            type:"pie",
            data:piedata,
        }],
    };
```

#### 2.常见效果

- 显示数值

  label.formatter

- 圆环

  设置两个圆环半径 radius:['50%','70%]

- 南丁格尔图

  roseType:'radius'

- 选中效果

  selectedMode:"single" 

  selectedOffset:30

  ```html
  <script>
      var myechart = echarts.init(document.getElementById("myechart"));
      var piedata =[
                  {value: 1048, name: '搜索引擎'},
                  {value: 735, name: '直接访问'},
                  {value: 580, name: '邮件营销'},
                  {value: 484, name: '联盟广告'},
                  {value: 300, name: '视频广告'}
              ],//数据为键值对形式
      option = {
          series:[{
              type:"pie",
              data:piedata,
              label:{
                  formatter:function(arg){
                  console.log(arg)
                  return arg.name+'平台'+arg.value + '元\n'+arg.percent+'%'
              } // 通过label中的formatter进行标签格的更改
              },
              // radius:50,
              // radius:["50%",'70%'],// 半径参考的是1/2*min[height,width] ,此处生成环装饼图，
              roseType:'radius', // 设置成南丁格尔图，即饼图的半径不一样，此处半径取决于数值大小
              selectedMode:"single" ,//选中，点击出现偏离，如果设置为multiple，可以进行多个的操作
              selectedOffset:30, // 设置点击偏离的距离
          }],
      };
      myechart.setOption(option)
  </script>
  ```

  ### 

  

#### 3.饼图特点

​	饼图可以帮助用户很好的了解各个分类的占比情况

### 2.9地图

#### 1.地图使用方式：

1. 百度地图api

   需要申请一个百度地图ak

2. 矢量地图

   需要提前准备矢量地图数据

#### 2.步骤

1. echarts基本结构

2. 准备中国的矢量地图json文件，放到json/map目录中

3. 使用ajax获取china.json

   $.get('json/map/china.json',function(china.json){})

4. 在回调函数中往echarts全局对象注册地图的json数据

   echarts.registerMap('**chinaMap**'，chinajson)

5. 在geo下配置

   type:"map",

   map:"**chinaMap**"

   ```html
   <script src="../static/js/echarts.min.js"></script>
   <script src="../static/js/jquery-3.5.1.min.js"></script>
   <script>
       var myechart = echarts.init(document.getElementById("myechart"));
       $.get('../static/geojson/guangdong.json',function(ret){
           // console.log(ret) //ret为各个地区的
           echarts.registerMap('guangdong',ret)
           var option={
               geo:{
                   type:'map',
                   map:"guangdong" //需要与registerMap第一个参数保持一致
               }
           }
           myechart.setOption(option)
       })
       
   </script>
   ```

   

#### 3.常用配置

1. 缩放拖动 roam
2. 名称显示 label：{show：true}
3. 初始显示放大 zoom
4. 地图中心点设置 center=[30.11,121.02]

```html
<script src="../static/js/echarts.min.js"></script>
<script src="../static/js/jquery-3.5.1.min.js"></script>
<script>
    var myechart = echarts.init(document.getElementById("myechart"));
    $.get('../static/geojson/guangdong.json',function(ret){
        console.log(ret) //ret为各个地区的
        echarts.registerMap('guangdong',ret)
        var option={
            geo:{
                type:'map',
                map:"guangdong", //需要与registerMap第一个参数保持一致
                zoom:3,
                label:{
                    show:true,

                },
                center:[113.382391, 22.521113],// 中山市位于地图的中央

            }
        }
        myechart.setOption(option)
    })
    
</script>
```

4.常见效果

- 不同城市颜色不同

  1.显示基本的中国地图

  2.城市的空气质量数据设置给series

  3.将series下的数据和geo关联起来

  4.结合visualMap配合使用

