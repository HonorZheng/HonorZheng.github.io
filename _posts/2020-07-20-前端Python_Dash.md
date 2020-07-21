---
title: Dash
layout: post
tags: 前端
categories: ''
---

# Dash

## 1. 安装

```bash
pip install dash
pip install dash-daq     # Dash核心后端
```

上述安装时，会自动安装dash-renderer，dash-core-components，dash-html-components和dash-table；

### 配置Jupyter notebook

```undefined
pip install jupyter_plotly_dash
```

安装成功后，如果在Jupyter notebook运行结果出现404错误，进行如下操作

```bash
conda install -c conda-forge jupyter-server-proxy
jupyter serverextension enable jupyter_server_proxy  # jupyter-server-proxy服务器扩展在安装时没有自
```

## 2.布局

Dash应用程序由两部分组成。第一部分是布局(layout)，描述应用程序的设计样式；第二部分描述了应用程序的交互性。

Dash为应用程序的所有可视化组件，提供了Python类，在`dash_core_components`库和`dash_html_components`库中，进行组件的维护。当然，也可以使用 [JavaScript 和 React.js](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fplotly%2Fdash-components-archetype) 构建自己的组件。

导入本章所有用到的包，下文不再说明

```python
import pandas as pd
import plotly.graph_objs as go
import dash
import dash_core_components as dcc                  # 交互式组件
import dash_html_components as html                 # 代码转html
from dash.dependencies import Input, Output         # 回调
from jupyter_plotly_dash import JupyterDash         # Jupyter中的Dash，如有疑问，见系列文章第2篇【安装】
```





