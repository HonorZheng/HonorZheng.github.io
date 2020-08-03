---
title: Dash(安装布局)
layout: post
tags: 前端
categories: ''
---

# Dash -纯python语言web开发

## 1. 安装

使用venv 进行python 环境管理

- 初始化venv 项目

```
python3 -m venv venv
```

- 激活环境

```
source   venv/bin/activate
```

- 添加依赖

```
pip install dash -i https://pypi.tuna.tsinghua.edu.cn/simple/
pip install dash-daq -i https://pypi.tuna.tsinghua.edu.cn/simple/
```

## 2.布局

### 2.1 柱状图显示

```python
import dash
import flask
import dash_core_components as dcc
import dash_html_components as html

server = flask.Flask(__name__)
external_stylesheets = ['https://codepen.io/chriddyp/pen/bWLwgP.css']
app = dash.Dash(__name__, external_stylesheets=external_stylesheets)
server = app.server
app.layout = html.Div(children=[
    html.H1(children='Hello Dash'),
    html.Div(children='''
        Dash: A web application framework for Python.
    '''),
    dcc.Graph(
        id='example-graph',
        figure={
            'data': [
                {'x': [1, 2, 3], 'y': [4, 1, 2], 'type': 'bar', 'name': 'SF'},
                {'x': [1, 2, 3], 'y': [2, 4, 5], 'type': 'bar', 'name': u'Montréal'},
            ],
            'layout': {
                'title': 'Dash Data Visualization'
            }
        }
    )
])

if __name__ == '__main__':
    app.run_server(debug=False)
```

![image-20200721170336594](C:\Users\zheng\AppData\Roaming\Typora\typora-user-images\image-20200721170336594.png)

1. 布局 **layout** 由 **html.Div** 和 **dcc.Graph** 这样的组件树组成；

2. Dash是 **声明式** 的，通过关键字参数描述组件。即Dash主要通过属性描述应用，如 style、className、id等；

3. **dash_html_components** 库为每个HTML标签都提供了对应的组件。本例中：`html.H1(children='Hello Dash')`可以生成`<h1>你好，Dash</h1>`这样的HTML语句。并非所有组件都使用纯HTML语言；

4. **dash_core_components** 这种交互式高阶组件库，是由JavaScript、HTML和CSS编写，并由React.js库生成，用于设置互动性图表组件，如控件、图形等，其语法类似Plotly；

5. 按照惯例，**children** 始终是第一个属性，可以省略，即 **html.H1(children='Hello Dash')** 和 **html.H1('Hello Dash')**相同，本例中，声明了3次，实际上都可以忽略。另外，它还可以包含字符串、数字、单个组件或组件列表。

   ------

   

### 2.2 表格显示

```python
'''
表格操作
'''
import pandas as pd
import plotly.graph_objs as go
import dash
import dash_core_components as dcc                  # 交互式组件
import dash_html_components as html                 # 代码转html
from dash.dependencies import Input, Output         # 回调
from jupyter_plotly_dash import JupyterDash

df = pd.read_csv(r"D:\02_Task\07_EdgeTech\10_Dash\ex_file\示例数据文件.csv")


# 定义表格组件
def create_table(df, max_rows=12):
    """基于dataframe，设置表格格式"""

    table = html.Table(
        # Header
        [
            html.Tr(
                [
                    html.Th(col) for col in df.columns
                ]
            )
        ] +
        # Body
        [
            html.Tr(
                [
                    html.Td(
                        df.iloc[i][col]
                    ) for col in df.columns
                ]
            ) for i in range(min(len(df), max_rows))
        ]
    )
    return table


# 设置Dash应用程序
external_stylesheets = ['https://codepen.io/chriddyp/pen/bWLwgP.css']

app = dash.Dash(__name__, external_stylesheets=external_stylesheets)
app.layout = html.Div(
    children=[
        html.H4(children='华电云南龙陵金星山项目风速'),
        create_table(df)
    ]
)

if __name__ == '__main__':
    app.run_server(debug=True)
```

![image-20200721170117188](C:\Users\zheng\AppData\Roaming\Typora\typora-user-images\image-20200721170117188.png)

1. **dash_html_components** 库除了为HTML参数提供了关键字外，还为每个HTML标签提供了组件类；
2. 示例中，使用 **style** 属性修改了 **html.Div** 和 **html.H1components** 行内样式；
3. **dash_html_components** 的 **HTML** 属性，与 **HTML** 属性之间存以下几点差异：

- HTML中的style属性是以分号分隔的字符串；Dash用的是字典；

- Dash的style字典键是 **camelCased(驼峰式)** 命名法，**HTML** 中的 **text-align**，在style字典中为 **textAlign**；

- **HTML** 的 **class** 属性，对应Dash中的 **className**；

- **HTML** 的子项是通过 **children**关键字参数指定的，按照惯例，这始终是第一个参数，经常被省略；

- 除了上述外，其他所有HTML属性与标签，在Python中都有效

  ------

  

### 2.3 组件显示

```python
import pandas as pd
import plotly.graph_objs as go
import dash
import dash_core_components as dcc  # 交互式组件
import dash_html_components as html  # 代码转html
from dash.dependencies import Input, Output  # 回调
from jupyter_plotly_dash import JupyterDash

# 设置Dash应用程序
external_stylesheets = ['https://codepen.io/chriddyp/pen/bWLwgP.css']

app = dash.Dash(__name__, external_stylesheets=external_stylesheets)
app.layout = html.Div([
    html.Label('下拉菜单'),
    dcc.Dropdown(
        options=[{'label': '北京', 'value': '北京'},
                 {'label': '天津', 'value': '天津'},
                 {'label': '上海', 'value': '上海'}],

        value='北京'),

    html.Label('多选下拉菜单'),
    dcc.Dropdown(
        options=[{'label': '北京', 'value': '北京'},
                 {'label': '天津', 'value': '天津'},
                 {'label': '上海', 'value': '上海'}],
        value=['北京', '上海'],
        multi=True),

    html.Label('单选钮'),
    dcc.RadioItems(
        options=[{'label': '北京', 'value': '北京'},
                 {'label': '天津', 'value': '天津'},
                 {'label': '上海', 'value': '上海'}],
        value='北京'),

    html.Label('多选框'),
    dcc.Checklist(
        options=[{'label': '北京', 'value': '北京'},
                 {'label': '天津', 'value': '天津'},
                 {'label': '上海', 'value': '上海'}],
        value=['北京', '上海']),

    html.Label('Text Input'),
    dcc.Input(value='天津', type='text'),

    html.Label('文本输入'),
    dcc.Slider(
        min=0, max=9, value=5,
        marks={i: '标签 {}'.format(i) if i == 1 else str(i) for i in range(1, 6)})
], style={'columnCount': 2})

if __name__ == '__main__':
    app.run_server(debug=True)

```

![image-20200721170017183](C:\Users\zheng\AppData\Roaming\Typora\typora-user-images\image-20200721170017183.png)

1. 示例中，展示了下拉列表单选、下拉列表多选、单选按钮、多选按钮、文本输入框、滑动条；

2. **dash_core_components** 包含一系列高级别的组件，如下拉列表、图形、Markdown文本等；

3. 与所有Dash组件一样，这些组件都是声明式的，组件的关键字参数也一样，每个选项都可以进行配置；

4. 在[Dash核心组件库中](https://links.jianshu.com/go?to=https%3A%2F%2Fdash.plot.ly%2Fdash-core-components)，可以查看所有可用的组件。

   ------

   

### 2.4 总结

1. 1. Dash组件是声明式的，在实例化关键字参数时，可设置配置项。通过调用help，可以查看Dash组件及其可用参数的更多信息；

2. ```bash
   help(dcc.Dropdown)
   ```

3. - 布局(**layout**)用来设置Dash应用程序的样式，是结构化的树状组件；
   - **dash_html_components** 库提供了所有的HTML标签和关键字参数，用来设置HTML属性，如style、className、id等；
   - **dash_core_components** 库生成了更高级别的组件，如控件和图形；
   - 具体参考官方文档：[dash_core_components](https://links.jianshu.com/go?to=https%3A%2F%2Fdash.plot.ly%2Fdash-core-components)、[dash_html_components](https://links.jianshu.com/go?to=https%3A%2F%2Fdash.plot.ly%2Fdash-html-components)



作者：惑也
链接：https://www.jianshu.com/p/ca1b2ae4883e
来源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。



