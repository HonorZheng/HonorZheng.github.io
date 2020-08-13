---
title: echarts和json格式
layout: post
tags: 前端
categories: ''
---

# JSON格式文件解析

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



# echars实现动态图表

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

## 1.基础教程

1.布局设置 ，使用flexible.css布局





