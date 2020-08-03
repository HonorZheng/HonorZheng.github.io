---
title: Dash(基本回调)
layout: post
tags: 前端
categories: ''
---

```python
app = JupyterDash('Dash Layout')

app.layout = html.Div([
    dcc.Input(id = 'my-id', value = '初始值', type = 'text'),
    html.Div(id = 'my-div')
])

@app.callback(
    Output(component_id = 'my-div', component_property = 'children'),
    [Input(component_id = 'my-id', component_property = 'value')]
)

def update_output_div(input_value):
    return '你输入了"{}"'.format(input_value)

```

![image-20200722085756157](C:\Users\zheng\AppData\Roaming\Typora\typora-user-images\image-20200722085756157.png)

1. 文本框中输入文字，输出组件的子项会立即更新。效果图显示，第一个设置的默认值，后两个，分布输入了数值100和字符串Dash；
2. **app.callback** 装饰器通过声明，描述应用程序界面的“输入”与“输出”项；
3. Dash中应用程序的【输入】和【输出】只是特定组件的属性。本例中，输入项是ID名为my-id 组件的value特性。 输出项是ID名为my-div 组件的children特性；
4. 当输入项组件的属性值，发生更改时，将自动调用callback装饰器打包的函数，将更新的内容，作为输入项参数，返回函数的输入内容，更新输出项组件的属性值；
5. 【输入项】和【输出项】对象的关键字参数 **component_id** 和 **component_property**，都是可选的。本例中，为了便于理解，列出了这两个关键字，通常情况下，为了让代码简明、易读，可以省略这两个关键字；
6. 不要混淆 **dash.dependencies.Input** 与**dash_core_components.Input**对象。前者只在回调函数中使用，后者才是真正的组件；
7. Dash应用程序启动时，会自动使用输入组件的初始值，调用所有的回调函数，以填充输出组件的初始值。所以，不要在layout中设置 my-div组件的children特性，本例中，如果指定了 **html.Div(id='my-div', children='Hello world')** 的内容，应用启动时会被覆盖。这种方式类似于Microsoft Excel编程：当单元格的内容发生变化时，依赖于该单元格的所有单元格的内容，都将自动更新。这称为 **“反应式编程” (Reactive Programming)** 。



作者：惑也
链接：https://www.jianshu.com/p/cb0dc98e00bc
来源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。