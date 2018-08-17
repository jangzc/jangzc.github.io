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
```
将指定特征的特征值等于 value 的行省下列作为子数据集
```
```
def splitDataSet(dataSet,index,value):
    '''
        splitDataSet(通过遍历dataSet数据集，求出index对应的column列的值为value的行)
        就是依据index列进行分类，如果index列的数据等于value的时候，就要将index划分到我们创建的新的数据集中
    Args:
        dataSet 数据集                    待划分的数据集
        index 表示每一行的index列         划分数据集的特征
        value 表示index列对应的value值    需要返回的特征的值
    Returns:
        index列为value的数据集【该数据集需要排除index列】
    '''
    # -----------切分数据集的第一种方式 start------------------------------------
    retDataSet = []
    for featVec in dataSet:
        # index列为value的数据集【该数据集需要排除index列】
        # 判断index列的值是否为value
        if featVec[index] == value:
            # [:index]表示前index行，即若index为2，就是取featVec的前index行
            reducedFeatVec = featVec[:index]
            '''
            extend和appaend的区别
            list.append(object)向列表中添加一个对象object
            list.extend(sequeue)把一个序列seq的内容添加到列表中
            1、使用append的时候，是将new_media看作一个对象，整体打包添加到music_media对象中
            2、使用extend的时候，是将new_media看作一个序列，将这个序列和music_media序列合并，并放在其后面
            result = []
            result.extend([1,2,3])
            print result
            result.append([4,5,6])
            print result
            result.extend([7,8,9])
            print result
            结果:
            [1,2,3]
            [1,2,3,[4,5,6]]
            [1,2,3,[4,5,6],7,8,9]
            '''
            reducedFeatVec.extend(featVec[index+1:])
            # [index+1:]表示从跳过index的index+1行，取接下来的数据
            # 收集结果值 index列为value的行【该行需要排除index列】
            retDataSet.append(reducedFeatVec)
    # -----------切分数据集的第一种方式 end------------------------------------
    
    # -----------切分数据集的第二种方式 start------------------------------------
    # retDataSet = [data for data in dataSet for i,v in enumerate(data) if i == axis and v ==value]
    # -----------切分数据集的第二种方式 end------------------------------------
    return retDataSet
```

选择最好的数据集划分方式
```
def chooseBestFeatureToSplit(dataSet):
    '''chooseBestFeatureToSplit(选择最好的特征)
    
    Args: dataSet 数据集
    Returns: bestFeature 最优的特征列
    '''
    # 求第一行有多少列的Feature，最后一列是label列
    numFeatures = len(dataSet[0]) - 1
    # 数据集的原始信息熵
    baseEntropy = calcShannonEnt(dataSet)
    # 最优的信息增益值，和最优的Feature编号
    bestInfoGain, bestFeature = 0.0, -1
    # iterate over all the features
    for i in range(numFeatures):
        # 获取对应的feature下的所有数据
        featList = [example[i] for example in dataSet]
        # 获取剔重后的集合，使用set对list数据进行去重
        uniqueVals = set(feaList)
        # 创建一个临时的信息熵
        newEntropy = 0.0
        # 遍历有一列的value集合，计算该列的信息熵
        # 遍历当前特征中的所有唯一属性值，对每个唯一属性值划分一次数据集，计算数据集的新熵值，并对所有唯一特征值得到的熵求和。
        for value in uniqueVals:
            subDataSet = splitDataSet(dataSet, i ,value)
            # 计算概率
            prob = len(subDataSet)/float(len(dataSet))
            # 计算信息熵
            newEntropy += prob * calcShannonEnt(subDataSet)
        # gain[信息增益]：划分数据集前后的信息变化，获取信息熵最大的值
        # 信息增益是熵的减少或者是数据无序度的减少。最后，比较所有特征中的信息增益，返回最好特征划分的索引值
        infoGain = baseEntropy - newEntropy
        print 'infoGain=', infoGain, 'bestFeature=',i,baseEntropy,newEntropy
        if(infoGain > bestInfoGain):
            bestInfoGain = infoGain
            bestFeature = i
    return bestFeature
```
```
问: 上面的 newEntropy 为什么是根据子集计算的呢？
答：因为我们在根据一个特征计算香农熵的时，该特征的分类值是相同的，这个特征这个分类的香农熵为0；
```

## 2.4 训练算法: 构造树的数据结构
```
def createTree(dataSet, labels):
    classList = [example[-1] for example in dataSet]
    # 如果数据集的最后一列的第一个值出现的次数=整个集合的数量，也就是说只有一个类别，就直接返回结果
    # 第一个停止条件：所有的类标签完全相同，则直接返回该类标签
    # count()函数是统计括号中的值在list中出现的次数
    if classList.count(classList[0]) == len(classList):
        return classList[0]
    #如果数据集中只有1列，那么最初出现的Label次数最多的一类，最为结果
    # 第二个停止条件：使用完了所有特征，仍然不能将数据集划分成仅包含唯一类别的分组。
    if len(dataSet[0]) == 1:
        return majorityCnt(classList)
    
    # 选择最优的列，得到最优对应的label含义
    bestFeat = chooseBestFeatureToSplit(dataSet)
    # 获取label的名称
    bestFeatLabel = labels[bestFeat]
    # 初始化myTree
    myTree = {bestFeatLabel:{}}
    # 注：labels列表是可变对象，在PYTHON函数中作为参数时传址引用，能够被全局修改
    # 所以这行代码导致函数外的同名变量被删除了元素，造成例句无法执行，提示'no surfacing' is not in list
    del(labels[bestFeat])
    # 取出最优列，然后它的branch做分类
    featValues = [example[bestFeat] for example in dataSet]
    uniqueVals = set(featValues)
    for value in uniqueVals:
        # 求出生育的标签label
        subLables = labels[:]
        # 遍历当前选择特征包含的所有属性值，在每个数据集划分上递归调用函数createTree()
        myTree[bestFeatLabel][value] = createTree(splitDataSet(dataSet, bestFeat,value),subLables)
        print 'myTree',value,myTree
    return myTree
```
## 2.5 测试算法：使用决策树执行分类
```
def classify(inputTree, featLabels, testVec):
    '''classify(给输入的节点，进行分类)
    Args:
        inputTree      决策树模型
        featLabels     Feature标签对应的名称
        testVec        测试输入的数据
    Returns:
        classLabel     分类的结果值，需要映射label才能知道名称
    '''
    # 获取tree的根节点对于的key值
    firstStr = inputTree.keys()[0]
    # 通过key得到根节点对应的value
    secondDict = inputTree[firstStr]
    # 判断跟接待你名称获取节点在label中的先后顺序，这样就知道输入的testVec怎么开始对照树来做分类
    featIndex = featLabels.index(firstStr)
    # 测试数据，找到根节点对应的label位置，也就知道从出入的数据的第几位来开始分类
    key = testVec[featIndex]
    valueOfFeat = secondDict[key]
    print '+++', firstStr,'xxx',secondDict,'---',key,'>>>',valueOfFeat
    # 判断分支是否结束：判断valueOffFeat是否是dict类型
    if isinstance(valueOfFeat, dict):
        classLabel = classify(valueOfFeat, featLabels, testVec)
    else:
        classLabel = valueOfFeat
    return classLabel
```
```
def fishTest():
    #1. 创建数据和结果标签
    myDat, labels = createDataSet()
    print myDat, labels
    
    # 计算label分类标签的香农熵
    # calcShannonEnt(myDat)
    
    # 求第0列为 1/0的列的数据集【排除第0列】
    print '1---',splitDataSet(myDat,0,1)
    print '0---',splitDataSet(myDat,0,0)
    
    # 计算最好的信息增益列
    print chooseBestFeatureToSplit(myDat)
    
    import copy
    myTree = createTree(myDat, copy.deepcopy(labels))
    print myTree
    # [1,1]表示要取的分支上的节点位置，对应的结果值
    print classify(myTree, labels, [0,1])
    
    # 获得树的高度
    
    # 画图可视化展现
    createPlot(myTree)
```
## 2.6 使用算法：此步骤可以适用于任何监督学习任务，而使用决策树可以更好地理解数据的内在含义
