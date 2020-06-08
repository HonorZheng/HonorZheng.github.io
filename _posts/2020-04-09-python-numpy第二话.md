---
title: python-numpy第二话
layout: post
tags: python-numpy
categories: ''
---
### 1. numpy.array() 矩阵生成(一维数组和二维矩阵)

    >>>
    #  numpy.array() 能输入一个list，一个list就是一维数组
    vector = numpy.array([5, 10, 15, 20])
    # 多个list输入就是多维数组
    matrix = numpy.array([[5, 10, 15], [20, 25, 30], [35, 40, 45]])
    print(vector)
    print(matrix) 
    >>>
    [ 5 10 15 20]
    [[ 5 10 15]
     [20 25 30]
     [35 40 45]]
     
#### 2. np.shape (查看数组维度)

    #We can use the ndarray.shape property to figure out how many elements are in the array
    vector = numpy.array([1, 2, 3, 4])
    print(vector.shape)
    #For matrices, the shape property contains a tuple with 2 elements.
    matrix = numpy.array([[5, 10, 15], [20, 25, 30]])
    print(matrix.shape)
    
#### 3. np.dtype (查看数组中数据类型)     
    numbers = numpy.array([1, 2, 3, 4])
    numbers.dtype
    
#### 4. np[] (切片操作，提取数据)  

    >>>
    matrix = numpy.array([
                        [5, 10, 15], 
                        [20, 25, 30],
                        [35, 40, 45]
                     ])
    print(matrix[1:3,0:2])
    >>>
    [[20 25]
    [35 40]]

#### 4. np的布尔运算  
    
    >>>
    vector = numpy.array([5, 10, 15, 20])
    vector == 10
    >>>
    array([False,  True, False, False])

#### 5. np布尔运算的选取功能[1]
    
    >>>
    # Compares vector to the value 10, which generates a new Boolean vector [False, True, False, False]. 
    #It assigns this result to equal_to_ten
    vector = numpy.array([5, 10, 15, 20])
    equal_to_ten = (vector == 10)
    print (equal_to_ten)
    print(vector[equal_to_ten])
    >>>
    [False  True False False]
    [10]

#### 6. np布尔运算的选取功能[2]-布尔集取值
    # 对第二列中数值等于25的作出布尔集
    >>>
    matrix = numpy.array([
                    [5, 10, 15], 
                    [20, 25, 30],
                    [35, 40, 45]
                 ])
    second_column_25 = (matrix[:,1] == 25)
    print (second_column_25)
    # 用布尔值代表行列，第二行值为True,这样表示代表第二行
    print(matrix[second_column_25, :])
    >>>
    [False  True  False]
    [[20 25 30]]
#### 7. np布尔运算的选取功能[3]-复合项布尔运算
    >>>
    #We can also perform comparisons with multiple conditions
    vector = numpy.array([5, 10, 15, 20])
    equal_to_ten_and_five = (vector == 10) | (vector == 5)
    print (equal_to_ten_and_five)
    >>>
    [ True True False False]
    --------------------------------------------------------
    >>> 将数组中5和10赋值为50
    vector = numpy.array([5, 10, 15, 20])
    equal_to_ten_or_five = (vector == 10) | (vector == 5)
    vector[equal_to_ten_or_five] = 50
    print(vector)
    >>>
    [50 50 15 20]
#### 7. np数组数据类型的改变
    >>>
    #We can convert the data type of an array with the ndarray.astype() method.
    vector = numpy.array(["1", "2", "3"])
    print (vector.dtype)
    print (vector)
    vector = vector.astype(float)
    print (vector.dtype)
    print (vector)
    >>>
    <U1
    ['1' '2' '3']
    float64
    [1. 2. 3.]

#### 7. np数学运算
    # 一维数组求和
    vector = numpy.array([5, 10, 15, 20])
    vector.sum()
    
    # 二维数组求和
    # The axis dictates which dimension we perform the operation on
    # 1 means that we want to perform the operation on each row, and 0 means on each column
    # axis =0 is rows. axis =1 is columns.
    
    >>>
    matrix = numpy.array([
                    [5, 10, 15], 
                    [20, 25, 30],
                    [35, 40, 45]
                 ])
    >>> matrix.sum(axis=1)
    >>> array([ 30,  75, 120])
    
    >>> matrix.sum(axis=0)
    >>> array([60, 75, 90])
 
#### 7. np替换空值
    #replace nan value with 0
    >>>
    world_alcohol = numpy.genfromtxt("world_alcohol.txt", delimiter=",")
    print(world_alcohol)
    >>>
    [[      nan       nan       nan       nan       nan]
     [1.986e+03       nan       nan       nan 0.000e+00]
     [1.986e+03       nan       nan       nan 5.000e-01]
     ...
     [1.987e+03       nan       nan       nan 7.500e-01]
     [1.989e+03       nan       nan       nan 1.500e+00]
     [1.985e+03       nan       nan       nan 3.100e-01]]
    --------------------------------------------------------------------
    >>> 对第五列进行赋值为0
    is_value_empty = numpy.isnan(world_alcohol[:,3])
    # print (is_value_empty)
    world_alcohol[is_value_empty, 3] = '0'
    print(world_alcohol)
    >>>
    [[      nan       nan       nan       nan 0.000e+00]
     [1.986e+03       nan       nan       nan 0.000e+00]
     [1.986e+03       nan       nan       nan 5.000e-01]
     ...
     [1.987e+03       nan       nan       nan 7.500e-01]
     [1.989e+03       nan       nan       nan 1.500e+00]
     [1.985e+03       nan       nan       nan 3.100e-01]]
    
    --------------------------------------------------------------------
    >>> 对第五列进行数据类型转换为浮点型，并求最大值和平均值    
    alcohol_consumption = world_alcohol[:,4]
    alcohol_consumption = alcohol_consumption.astype(float)
    total_alcohol = alcohol_consumption.sum()
    average_alcohol = alcohol_consumption.mean()
    print (total_alcohol)
    print (average_alcohol)
    >>>
    1137.78
    1.140060120240481
    
    
####  由于数组的滑动，数据量发生重叠而增加，此处代码用于将重叠区域的风速取平均，并整合成
####  step 1,将二维数组进行滑动平均，滑动长度为timeslip，用于生成多个独立的而二维预测数据

```
def array_split(data, timeslip):
    slice = []
    for i in range(int(len(data) / timeslip)):
        slice.append(trainPredict[i * timeslip:(i + 1) * timeslip])
    return np.array(slice)
```

#### step 2,对三维数组进行滑动的平均，平均方式为阶梯型，阶梯值为1，代表连续

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
