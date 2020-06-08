---
title: python-numpy第三话
layout: post
tags: python-numpy
categories: ''
---
#### 1. numpy 生成特殊矩阵操作
    >>>
    import numpy as np
    a = np.arange(15).reshape(3, 5)
    a
    >>>
    array([[ 0,  1,  2,  3,  4],
           [ 5,  6,  7,  8,  9],
           [10, 11, 12, 13, 14]])
           
    >>> np.zeros ((3,4))  
    >>>
     array([[0., 0., 0., 0.],
           [0., 0., 0., 0.],
           [0., 0., 0., 0.]])
           
    >>> np.ones( (2,3,4), dtype=np.int32 )
        array([[[1, 1, 1, 1],
                [1, 1, 1, 1],
                [1, 1, 1, 1]],
    
               [[1, 1, 1, 1],
                [1, 1, 1, 1],
                [1, 1, 1, 1]]])
                
#### 2. numpy 生成矩阵 （arrange，random，linspace）
    >>> 等间隔生成(间隔为5)      
    #To create sequences of numbers, the last is step
    np.arange( 10, 30, 5 )  
    >>> array([10, 15, 20, 25])
    
    >>> 按个数生成(5个）
    from numpy import pi
    >>> np.linspace( 0, 2*pi, 5 )
    >>>
    array([0.        , 1.57079633, 3.14159265, 4.71238898, 6.28318531])
    
#### 3.numpy 矩阵运算（加法，点乘）
    >>> 加法运算
    #the product operator * operates elementwise in NumPy arrays
    a = np.array( [20,30,40,50] )
    b = np.arange( 4 )
    print (a) 
    print (a<35)
    print (b)
    c = a-b
    print (c)
    >>>
    [20 30 40 50]
    [ True  True False False]
    [0 1 2 3]
    [20 29 38 47]
    ----------------------------------------------------------------
    #The matrix product can be performed using the dot function or method
    >>> 矩阵点乘(两种形式皆可)
    A = np.array( [[1,1],
                   [0,1]] )
    B = np.array( [[2,0],
                   [3,4]] )
    print( A)
    print( B)
    #print A*B
    print (A.dot(B))
    print (np.dot(A, B)) 
    >>>
    [[1 1]
     [0 1]]
     
    [[2 0]
     [3 4]]
     
    [[5 4]
     [3 4]]
     
    [[5 4]
     [3 4]]