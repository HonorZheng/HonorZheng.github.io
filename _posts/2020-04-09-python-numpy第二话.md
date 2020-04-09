---
title: python-numpy第二话
layout: post
tags: pyhon-numpy
categories: ''
---
# todo 由于数组的滑动，数据量发生重叠而增加，此处代码用于将重叠区域的风速取平均，并整合成
# todo step 1,将二维数组进行滑动平均，滑动长度为timeslip，用于生成多个独立的而二维预测数据

```
def array_split(data, timeslip):
    slice = []
    for i in range(int(len(data) / timeslip)):
        slice.append(trainPredict[i * timeslip:(i + 1) * timeslip])
    return np.array(slice)
```

# todo step 2,对三维数组进行滑动的平均，平均方式为阶梯型，阶梯值为1，代表连续

```
def slide_mean(data, timeslip):
    # 构造空矩阵 data.shape[0]为长度，由于滑动timeslip,新的矩阵长度增加
    meanvalue = np.zeros((data.shape[0], data.shape[2]))
    # 4 8 5
    data_3D = np.zeros((data.shape[1], timeslip, data.shape[2]))
    for i in range(data.shape[0]):
        # todo 实现滑动数组方法，剃头发模式
        # 更新值
        data_3D[i % timeslip, 0:timeslip] = data[i]
        # 求均值
        meanvalue[i] = np.mean(data_3D[:, 0, :])
        # 剃头发
        data_3D = data_3D[:, 1:, :]
        # 补充维度
        b = np.zeros((data_3D.shape[0], 1, data_3D.shape[2]))
        data_3D = np.hstack((data_3D, b))
        # 如果一轮完全迭代
    return meanvalue
```