---
layout:     post
title:      决策树项目案例之一
subtitle:   《机器学习实战五》
date:       2018-08-09
author:     Jang
header-img: img/post-bg-debug.png
catalog: true
tags:
    - MachineLearning
    - 机器学习实战
---

# 1. 项目概述<br>
根据以下2个特征，将动物分成两类: 鱼类和非鱼类
特征：
* 1. 不浮出水面是否可以生存
* 2. 是否有脚蹼

# 2. 开发流程
```
收集数据：可以使用任何方法
准备数据：树构造算法（这里使用的是ID3算法，因此数值型数据必须离散化。）
分析数据：可以使用任何方法，构造树完成之后，我们可以将树画出来。
训练算法：构造树结构
测试算法：使用习得的决策树执行分类
使用算法：此步骤可以适用于任何监督学习任务，而使用决策树可以更好地理解数据的内在含义
```

## 2.1 收集数据:
我们利用createDataSet()函数输入数据：
```
def createDataSet():
    dataSet = [[1,1,'yes'],
            [1,1,'yes'],
            [1,0,'no'],
            [0,1,'no'],
            [0,1,'no']]
    labels = ['no surfacing', 'flippers']
    return dataSet, labels
```

## 2.2 准备数据：树构造算法
此处，由于我们输入的数据本身就是离散化数据，所以这一步就省略了。

## 2.3 分析数据：可以使用任何方法，构造树完成之后，我们可以将树画出来。
<img src="https://github.com/apachecn/MachineLearning/blob/master/images/3.DecisionTree/%E7%86%B5%E7%9A%84%E8%AE%A1%E7%AE%97%E5%85%AC%E5%BC%8F.jpg"/>

* 计算给定数据集的香农熵的函数
```
def calcShannonEnt(dataSet):
    '''
    计算给定数据集的香农熵
    args:
        dataSet 数据集
    return:
        返回每一组feature下的某个分类下，香农熵的信息期望
    '''
    # -----------计算香农熵的第一种实现方式start--------------------------------
    # 求list的长度，表示计算参与训练的数据量
    numEntries = len(dataSet)
    # 下面输出我们测试的数据集的一些信息
    # 例如: <type 'list'> numEntries: 5 是下面代码的输出
    # print type(dataSet), 'numEntries:', numEntries
    
    # 计算分类标签label出现的次数
    labelCounts = {}
    # the number of unique elements and their occurance
    for featVec in dataSet:
        # 将当前实例的标签存储，即每一行数据的最后一个数据代表的是标签
        currentLabel = featVec[-1]
        # 为所有可能的分类创建字典，如果当前的键值不存在，则扩展字典并将当前键值加入字典。
        # 每个键值都记录了当前类别出现的次数。
        if currentLabel not in labelCounts.keys():
            labelCounts[currentLabel] = 0
        labelCounts[currentLabel] += 1
        # print '------',featVec, labelCounts
    
    # 对于label标签的占比，求出label标签的香农熵
    shannonEnt = 0.0
    for key in labelCounts:
        # 使用所有类标签的发生频率计算类别出现的概率。
        prob = float(labelCounts[key])/numEntries
        # log base 2
        # 计算香农熵，以2为底求对数
        shannonEnt -= prob * log(prob,2)
        print '----', prob, prob * log(prob,2), shannonEnt
    # -----------计算香农熵的第一种实现方式end------------------------------------
    
    # -----------计算香农熵的第二种实现方式start--------------------------------
    # 统计标签出现的次数
    #label_count = Counter(data[-1] for data in dataSet)
    # 计算概率
    #probs = [p[1] / float(len(dataSet)) for p in label_count.items()]
    #print probs
    # 计算香农熵
    #shannonEnt = sum([-p * log(p,2) for p in probs])
    # -----------计算香农熵的第二种实现方式end--------------------------------
    return shannonEnt
```

* 按照给定特征划分数据集
