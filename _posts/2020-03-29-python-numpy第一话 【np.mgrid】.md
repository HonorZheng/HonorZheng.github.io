---
layout: post
title: 'numpy第一话  np.mgrid'
subtitle: ''
date: 2020-03-29
categories: 
cover: ''
tags: python-numpy
---


#  你应该知道numpy（第一话  np.mgrid）
* 2020-03-29

一、np的语法格式
---
```
np.mgrid[start:end:step]
参数解析：
 
    start:开始坐标
 
    stop:结束坐标（实数不包括，复数包括）
 
    step:步长
```
matplotlib绘制三维图表，里面都用到了numpy中的一个函数叫mgrid，下面介绍一下：<br>

用法：返回多维结构，常见的如2D图形，3D图形。

第1返回值为第1维数据在最终结构中的分布<br>
第2返回值为第2维数据在最终结构中的分布，以此类推。（分布以矩阵形式呈现）<br>

mgrid[[1:3:3j, 4:5:2j]]<br>
3j：3个点<br>


```
步长为复数表示点数，左闭右闭<br>
步长为实数表示间隔，左闭右开<br>
```


二、举例
---
* 例如1D结构（array），如下：
```
>>> import numpy as np
>>> x=np.mgrid[-5:5:5j]
>>> x
array([-5. , -2.5,  0. ,  2.5,  5. ])
```
* 例如2D结构 (2D矩阵)，如下：


```
>  import numpy as np
>  x,y=np.mgrid[-5:5:3j,-2:2:3j]
>  x
>  array([[-5., -5., -5.],
>         [ 0.,  0.,  0.],
>         [ 5.,  5.,  5.]])
>  y
>  array([[-2.,  0.,  2.],
>         [-2.,  0.,  2.],
>         [-2.,  0.,  2.]])
>   
```

注意：
观察x，其中x沿着水平向右的方向扩展(即是：每列都相同)。<br>
观察y，y沿着垂直的向下的方向扩展(即是：每行都相同)。<br>


```
>>> import numpy as np
>>> x,y=np.mgrid[-5:5:3j,-2:2:3]
>>> x
array([[-5., -5.],
       [ 0.,  0.],
       [ 5.,  5.]])
>>> y
array([[-2.,  1.],
       [-2.,  1.],
       [-2.,  1.]])
>>> 
```

* 例如3D结构 (3D立方体)，如下：?

```
>>> import numpy as np
>>> x,y,z=np.mgrid[-5:5:3j,-2:2:3j,-1:1:2]
>>> x
array([[[-5.],
        [-5.],
        [-5.]],
 
       [[ 0.],
        [ 0.],
        [ 0.]],
 
       [[ 5.],
        [ 5.],
        [ 5.]]])
>>> y
array([[[-2.],
        [ 0.],
        [ 2.]],
 
       [[-2.],
        [ 0.],
        [ 2.]],
 
       [[-2.],
        [ 0.],
        [ 2.]]])
>>> z
array([[[-1.],
        [-1.],
        [-1.]],
 
       [[-1.],
        [-1.],
        [-1.]],
 
       [[-1.],
        [-1.],
        [-1.]]])
>>> 
```

三、三维绘图


声明：k轴范围为1~3，b轴范围为4~6；<br>

步骤1：朝右扩展<br>

```
[1 1 1] 
[2 2 2] 
[3 3 3]
```

步骤2：朝下扩展

```
[4 5 6] 
[4 5 6] 
[4 5 6]
```

步骤3：定位（ki，bi），把上面的k、b联合起来

```
[(1,4) (1,5) (1,6)] 
[(2,4) (2,5) (2,6)] 
[(3,4) (3,5) (3,6)]
```

步骤4：将（ki，bi）代入f(k,b)=3k^2+2b+1求f(ki,bi)

```
[12 14 16] 
[21 23 25] 
[36 38 40]
```

代码如下：

```
import numpy as np
import matplotlib.pyplot as plt
import mpl_toolkits.mplot3d
import pylab as p
import mpl_toolkits.mplot3d.axes3d as p3
 
k,b=np.mgrid[1:3:3j,4:6:3j]
f_kb=3*k**2+2*b+1
 
k.shape=-1,1
b.shape=-1,1
f_kb.shape=-1,1 #统统转成9行1列
 
fig=p.figure()
ax=p3.Axes3D(fig)
ax.scatter(k,b,f_kb,c='r')
ax.set_xlabel('k')
ax.set_ylabel('b')
ax.set_zlabel('ErrorArray')
p.show()
```

运行结果：


步骤5：将（ki,bi,f(ki,bi)）连起来，形成曲面


```
import numpy as np
import matplotlib.pyplot as plt
import mpl_toolkits.mplot3d
import pylab as p
import mpl_toolkits.mplot3d.axes3d as p3
 
k,b=np.mgrid[1:3:3j,4:6:3j]
f_kb=3*k**2+2*b+1
 
ax=plt.subplot(111,projection='3d')
ax.plot_surface(k,b,f_kb,rstride=1,cstride=1)
ax.set_xlabel('k')
ax.set_ylabel('b')
ax.set_zlabel('ErrorArray')
p.show()

```

注意：mgrid中第三个参数越大，说明某一区间被分割得越细，相应的曲面越精准。在上面的例子中第三个参数为3j，如果说我们其它不变，

部分参考了作者：
————————————————
版权声明：本文为CSDN博主「炊烟袅袅岁月长」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/abc13526222160/java/article/details/88559162

