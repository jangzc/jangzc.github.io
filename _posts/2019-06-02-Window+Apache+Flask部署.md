---
layout:     post
title:      Windows+Apache+Flask部署
subtitle:   
date:       2019-06-02
author:     Jang
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - MachineLearning
---


## 1. 第一步：安裝Apache
https://www.apachelounge.com/download/

## 2. 第二步：安裝mod_wsgi
https://www.lfd.uci.edu/~gohlke/pythonlibs/#pil
注意apache版本中的vc号，py版本号需要与mod_wsgi对应




## 2. 期间遇到的问题
### 2.1 启动Apache httpd服务时，报错：
```
Invalid command 'Order', perhaps misspelled or defined by a module not included in the server configuration
```
解决方案:With Apache 2.4 please uncomment/add the following modules:
```
LoadModule access_compat_module modules/mod_access_compat.so
LoadModule authz_host_module modules/mod_authz_host.so
```
### 2.2 无法load the file system codec，是因为无法引入encodings模块造成的
解决方案:
```
1. 在PATH中增加路Python的相关路径
需要在PATH变量中增加%USERPROFILE%\AppData\Local\Programs\Python\Python35\Scripts和%USERPROFILE%\AppData\Local\Programs\Python\Python35。当然，这个可以在安装Python3.5的时候勾选一下就可以了，默认选项是不增加。
2. 设置PYTHONPATH
这个需要新增PYTHONPATH变量，值设置成“%USERPROFILE%\AppData\Local\Programs\Python\Python35\DLLs;%USERPROFILE%\AppData\Local\Programs\Python\Python35\Lib;%USERPROFILE%\AppData\Local\Programs\Python\Python35\Lib\site-packages”。
3. 增加PATHEXT增加Python脚本的扩展名
这个需要将.PY和.PYW增加到PATHEXT环境变量中。设置完成后执行Python脚本时，只需要输入文件名即可。
```

### 2.3 对于2.2的问题的补充:
如果使用的是anaconda的虚拟环境，需要把对应的环境变量切换成这个虚拟环境里的路径
