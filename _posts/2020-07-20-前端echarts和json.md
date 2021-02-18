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

#### 4.常见效果

- 不同城市颜色不同

  1.显示基本的中国地图

  2.城市的空气质量数据设置给series

  3.将series下的数据和geo关联起来

  4.结合visualMap配合使用

```html
<script>
    var myechart = echarts.init(document.getElementById("myechart"));
    var airdata =[
    {name: '广州市', value: 500},
    {name: '韶关市', value: 360},
    {name: '深圳市', value: 200},
    {name: '清远市', value: 532},
    {name: ' 东莞市', value: 454},
    {name: '珠海市', value: 223},
    {name: '汕头市', value: 231},
    {name: '江门市', value: 323},
    {name: '佛山市', value: 212},
    {name: '湛江市', value: 2321},
    {name: '茂名市', value: 2132},
    {name: '肇庆市', value: 231},
    {name: '惠州市', value: 231},
    {name: '梅州市', value: 321},
    {name: '汕尾市', value: 553},
    {name: '河源市', value: 554},
    {name: '阳江市', value: 321},
    {name: '中山市', value: 535},
    {name: '潮州市', value: 365},
    {name: '揭阳市', value: 456},
    {name: '云浮市', value: 453}
]
    $.get('../static/geojson/guangdong.json',function(ret){
        console.log(ret) //ret为各个地区的
        var a=[]
        ret.features.forEach(function(element) {
            console.log(element.properties.name);
            a.push(element.properties.name)
            });
            console.log(a);
        // console.log(ret.features[0].properties.name) //ret为各个地区的
        echarts.registerMap('guangdong',ret)
        var option={
            grid:{
                left:'10%',
                top:5000,
                borderColor:'red',
            },
            series:{data:airdata,
            geoIndex:0 ,// 将空气质量数据与第0个geo进行匹配
            type:"map",        
            },

            geo:{
                type:'map',
                map:"guangdong", //需要与registerMap第一个参数保持一致
                zoom:1,
                label:{
                    show:true,

                },

                center:[113.382391, 22.521113],// 中山市位于地图的中央
            },
            visualMap:{
                min:0,
                max:3000,
                inRange:{
                    color:['white','red'], //控制渐变色
                },
                calculable:true, //与max，min配合出现滑块效果

            },
        }
        myechart.setOption(option)
    })
</script>
```

- 地图与散点图结合

  1. 给series下增加新的对象

  2. 准备好散点数据，设置给新对象的data

  3. 配置新对象的type

     type:effectScatter

  4. 让散点图使用地图坐标系统

     coordinateSystem：“geo”

  5. 让涟漪的效果更加明显

     reppleEffect：{ scale:10}

```html
<script>
    var myechart = echarts.init(document.getElementById("myechart"));
    var scatterData = [
        {value:[113.382391, 22.521113]}
        ];//呈现涟漪动画的坐标点
    var airdata =[
    {name: '广州市', value: 500},
    {name: '韶关市', value: 360},
    {name: '深圳市', value: 200},
    {name: '清远市', value: 532},
    {name: ' 东莞市', value: 454},
    {name: '珠海市', value: 223},
    {name: '汕头市', value: 231},
    {name: '江门市', value: 323},
    {name: '佛山市', value: 212},
    {name: '湛江市', value: 2321},
    {name: '茂名市', value: 2132},
    {name: '肇庆市', value: 231},
    {name: '惠州市', value: 231},
    {name: '梅州市', value: 321},
    {name: '汕尾市', value: 553},
    {name: '河源市', value: 554},
    {name: '阳江市', value: 321},
    {name: '中山市', value: 535},
    {name: '潮州市', value: 365},
    {name: '揭阳市', value: 456},
    {name: '云浮市', value: 453}
]
    $.get('../static/geojson/guangdong.json',function(ret){
        console.log(ret) //ret为各个地区的
        var a=[]
        ret.features.forEach(function(element) {
            console.log(element.properties.name);
            a.push(element.properties.name)
            });
            console.log(a);
        echarts.registerMap('guangdong',ret)
        var option={
            geo:{
                type:'map',
                map:"guangdong", //需要与registerMap第一个参数保持一致
                zoom:1.2,
                label:{
                    show:true,

                },

                center:[113.382391, 22.521113],// 中山市位于地图的中央
            },
            series:[{
                data:airdata,
                geoIndex:0 ,// 将空气质量数据与第0个geo进行匹配
                type:"map",        
            },
            {
                data:scatterData,//配置散点数据
                type:'effectScatter', //配置散点类型
                coordinateSystem:"geo",//指明散点使用的坐标系统，为geo
                rippleEffect:{
                    scale:10
                }
            }],


            visualMap:{
                min:0,
                max:3000,
                inRange:{
                    color:['white','red'], //控制渐变色
                },
                calculable:true, //与max，min配合出现滑块效果
            },
        }
        myechart.setOption(option)
    })
    
</script>
```

#### 5.地图特点

地图主要可以帮助我们从宏观上快速看出不同地理位置上的数据差异

### 2.10雷达图

#### 1.实现步骤

- 定义各个维度的最大值
- 定义图表的类型

#### 2.雷达图特点

雷达图可以用来分析多个维度的数据与标准情况数据的对比情况

```html
<script>
    var myechart = echarts.init(document.getElementById("myechart"));
    option = {
    title: {
        text: '基础雷达图'
    },
    tooltip: {},
    label: {show:true},   //显示数值
    legend: {
        data: ['预算分配（Allocated Budget）', '实际开销（Actual Spending）']
    },
    radar: {
        // shape: 'circle',
        name: {
            textStyle: {
                color: '#fff',
                backgroundColor: '#999',
                borderRadius: 3,
                padding: [3, 5]
            }
        },
        indicator: [
            { name: '销售（sales）', max: 6500},   //配置各维度最大值
            { name: '管理（Administration）', max: 16000},
            { name: '信息技术（Information Techology）', max: 30000},
            { name: '客服（Customer Support）', max: 38000},
            { name: '研发（Development）', max: 52000},
            { name: '市场（Marketing）', max: 25000}
        ],
        shape:"circle" //雷达形状为圆形，默认是polygon


    }, //添加显示信息
    series: [{
        name: '预算 vs 开销（Budget vs spending）',
        type: 'radar',
        // areaStyle: {normal: {}}, //形成阴影面积区域
        data: [
            {
                value: [4300, 10000, 28000, 35000, 50000, 19000],
                name: '预算分配（Allocated Budget）'
            },
            {
                value: [5000, 14000, 28000, 31000, 42000, 21000],
                name: '实际开销（Actual Spending）'
            }
        ]
    }]
};
    myechart.setOption(option)
</script>

```

### 2.11仪表盘

```html
<script>
    // 1.echarts基本结构
    // 2.准备数据，配置series下的data
    // 3.将type设置为gauge
    var myechart = echarts.init(document.getElementById("myechart"));
    option = {
        series: [
            {
                type: 'gauge',
                data: [{            //配置双指针，配置data下多个对象
                    value: 75,
                    itemStyle: {
                        color:"pink"
                    }
                }, {
                    value: 50,
                    itemStyle: {
                        color: "black"
                    }
                }
                ],
                min: 20 //min和max控制数值范围
            },
        ]
    };
    myechart.setOption(option)
</script>
```

### 2.12七个基本图表小结

#### 1.各个图表的英文单词

bar、line、scatter、pie、map、radar、gauge

#### 2.上手基本步骤

- 引入
- 准备
- 设置

#### 3.常用图表差异

- options的差异
- 7个常用图表的配置
- API文档查看

## 三、echarts显示配置

#### 1.内置主题

- echars中默认内置两套主题：light、dark
- 在初始化对象方法init中可以指明

```javascript
var myechart = echarts.init(document.getElementById("myechart"),'light');
var myechart = echarts.init(document.getElementById("myechart"),'dark');
```

#### 2.自定义主题

1.在echarts官网中，设置主题，保存js文件，直接引用

2.初始化对象的时候，直接将主题改为保存文件的名字。这个主题名字取决于该js文件中，有个**echarts.registerTheme('itcast'，)**中的第一个参数。

```javascript
var myechart = echarts.init(document.getElementById("myechart"),'itcast');
```

#### 3.调色盘

它是一组颜色，图形、系列会自动从其中选择颜色

1. 主题调色盘

2. 全局调色盘

   ```javascript
   option={
   color:['red','green','blue']
   }
   ```

   

3. 局部调色盘

   ```javascript
   series:[{
   type:"bar",
   color:["red","green","blue"]
   }]
   ```

   调色盘遵循就近原则：局部>全局>主题

#### 4.颜色渐变

线性渐变

```javascript
series:{
data:...
itemStyle:{
color：{
type:'liner',
x:0,
y:0,
x2:0,
y2:1,		//从[0，0]向[0，1] 方向
colorStops:[
{offsete:0,color:'red'  // 在0出为红色
},
{offsete:0,color:'blue' // 在100%处为蓝色
}
]}
}

```

- 径向渐变

  ```javascript
  itemStyle:{
  color：{
  type:'radial',
  x:0.5,
  y:0.5,
  r:0.5,		//从[0，0]向[0，1] 方向
  colorStops:[
  {offsete:0,color:'red'  // 在0出为红色
  },
  {offsete:0,color:'blue' // 在100%处为蓝色
  }
  ],
  global:false //缺省为false
  }
  }
  ```

#### 5.样式

- 直接样式

1. itemStyle 控制区域块的颜色
2. textStyle 控制文字的样式
3. lineStyle 控制线型的样式
4. areaStyle 控制区域的样式
5. label 控制标签的样式

- 高亮样式

  emphasis中包裹itemStyle、textStyle、lineStyle、areaStyle、label

#### 6.自适应

当浏览器的大小发生变化时，图表也屏幕适配

1.监听窗口的大小发生变化事件

2.在事件处理函数中调用echarts实例对象resize方法

```javascript
window.onresize = myechart.resize
```

或者

```
window.onresize=function(){
myecharts.resize()
}
```

## 四、动画效果

#### 1. 加载动画

数据加载过程中的动画效果,在合适的时间加入动画，隐藏动画

- 显示加载动画

  myecharts.showLoading()

- 隐藏加载动画

  myecharts.hideLoading()

#### 2.增量动画

