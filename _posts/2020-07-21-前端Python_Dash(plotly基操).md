---
title: Dash(plotly基操)
layout: post
tags: 前端
categories: ''
---

## 1. 三种样式的折线图

```python
import plotly.offline as py
import numpy as np
import plotly.graph_objs as go
import pandas as pd

datasou = pd.read_csv('ex_file/示例数据文件.csv')
datasou = datasou.head(1000)
x = datasou.index.values.tolist()
y1 = datasou.iloc[:, 1]
y2 = datasou.iloc[:, 2]
y3 = datasou.iloc[:, 3]
# Create traces
trace0 = go.Scatter(
    x=x,
    y=y1,
    mode='markers',
    name='markers'
)
trace1 = go.Scatter(
    x=x,
    y=y2,
    mode='lines+markers',
    name='lines+markers'
)
trace2 = go.Scatter(
    x=x,
    y=y3,
    mode='lines',
    name='lines'
)
data = [trace0, trace1, trace2]
py.plot(data)
# 随机设置4个参数，x轴的数字和y轴，其中y轴随机3组数据。
# 然后画三种类型的图，trace0是markers，trace1是折线图和markers,trace3是折线图。
```

