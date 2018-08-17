---
layout:     post
title:      决策树项目案例之二
subtitle:   《机器学习实战六》
date:       2018-08-17
author:     Jang
header-img: img/post-bg-debug.png
catalog: true
tags:
    - MachineLearning
    - 机器学习实战
---

## 1. 项目概述<br>
隐形眼镜类型包括硬材质、软材质以及不适合佩戴隐形眼镜。我们需要使用决策树预测患者需要佩戴的隐形眼镜类型。

## 2. 开发流程<br>
* 1). 收集数据：提供的文本文件。
* 2). 解析数据: 解析tab键分隔的数据行
* 3). 分析数据：快速检查数据，确保正确地解析数据内容，使用createPlot()函数绘制最终的树形图
* 4). 训练算法：使用createTree()函数
* 5). 测试算法：编写测试函数验证决策树可以正确分类给定的数据实例
* 6). 使用算法：存储树的数据结构，以便下次使用时无序重新构造树

### 2.1 收集数据：提供的文本文件<br>
文本文件数据格式如下：
```
young	myope	no	reduced	no lenses
pre	myope	no	reduced	no lenses
presbyopic	myope	no	reduced	no lenses
```

### 2.2 解析数据：解析tab键分隔的数据行
```
lecses = [inst.strip().split('\t') for inst in fr.readlines()]
lensesLabels = ['age','prescript','astigmatic','tearRate']
```

### 2.3 分析数据
```
>>> treePlotter.createPlot(lensesTree)
```

### 2.4 训练算法
### 2.5 测试算法
### 2.6 使用算法
使用 pickle 模块存储决策树
```
def storeTree(inputTree, filename):
    import pickle
    # -------------- 第一种方法 start --------------
    fw = open(filename,'wb')
    pickle.dump(inputTree,fw)
    fw.close()
    # -------------- 第一种方法 end --------------
    
    # -------------- 第二种方法 start --------------
    with open(filename, 'wb') as fw:
        pickle.dump(inputTree,fw)
    # -------------- 第二种方法 end --------------

def grabTree(filename):
    import pickle
    fr = open(filename,'rb')
    return pickle.load(fr)
```


