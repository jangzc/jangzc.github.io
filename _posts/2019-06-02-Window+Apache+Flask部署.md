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
httpd.conf里添加内容:
```
LoadFile "D:/devtools/Anaconda2/envs/FPN_TF/python36.dll"
LoadModule wsgi_module "D:/devtools/Anaconda2/envs/FPN_TF/Lib/site-packages/mod_wsgi/server/mod_wsgi.cp36-win_amd64.pyd"
WSGIPythonHome "D:/devtools/Anaconda2/envs/FPN_TF/python"
```
## 3. 第三步：安裝flask
```
pip install falsk
```

## 4. 第四步:测试文件
```
et_test.py
from flask import *
app=Flask(__name__)
@app.route('/')
def index():
   return "eating test~~~"
if __name__ == '__main__':
   app.run()
```
```
et_test.wsgi
import sys, os
sys.path.insert(0, os.path.dirname(__file__))
from et_test import app
application = app
```
httpd.conf添加：
```
<VirtualHost *:80>
 DocumentRoot "C:\et_test"
  ServerName localhost
   <Directory "C:\et_test">
    Order allow,deny
    Allow from all
   </Directory>
  WSGIScriptAlias /et_web C:\et_test\et_test.wsgi
</VirtualHost>
```
并且注释以下内容:
```
<Directory />
  # AllowOverride none
  # Require all denied
</Directory>
```


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

### 2.4 python环境变量，path和pythonpath的使用
1. 系统python可以正常运行，conda可以运行，activate可以运行，http启动失败
```
Path=D:\devtools\Anaconda2\Scripts\;D:\devtools\Anaconda2\;C:\Program Files (x86)\Common Files\Oracle\Java\javapath;C:\ProgramData\Oracle\Java\javapath;C:\Windows\system32;C:\Windows;C:\Windows\System32\Wbem;C:\Windows\System32\WindowsPowerShell\v1.0\;C:\Program Files (x86)\NVIDIA Corporation\PhysX\Common;%JAVA_HOME%/bin;%JAVA_HOME%/jre/bin;D:\Program Files\TortoiseSVN\bin;D:\Program Files\VisualSVN Server\bin;C:\Program Files (x86)\Windows Kits\8.1\Windows Performance Toolkit\;C:\Program Files\Microsoft SQL Server\110\Tools\Binn\;C:\Program Files\Git\cmd
无PYTHONPATH
```
```
2. 系统python可正常运行(运行的其实是FPN_TF里的python)，conda不可以运行,activateb不可正常运行，http服务可以启动
Path=D:\devtools\Anaconda2\envs\FPN_TF\Scripts\;D:\devtools\Anaconda2\envs\FPN_TF\;C:\Program Files (x86)\Common Files\Oracle\Java\javapath;C:\ProgramData\Oracle\Java\javapath;C:\Windows\system32;C:\Windows;C:\Windows\System32\Wbem;C:\Windows\System32\WindowsPowerShell\v1.0\;C:\Program Files (x86)\NVIDIA Corporation\PhysX\Common;%JAVA_HOME%/bin;%JAVA_HOME%/jre/bin;D:\Program Files\TortoiseSVN\bin;D:\Program Files\VisualSVN Server\bin;C:\Program Files (x86)\Windows Kits\8.1\Windows Performance Toolkit\;C:\Program Files\Microsoft SQL Server\110\Tools\Binn\;C:\Program Files\Git\cmd
PYTHONPATH=D:\devtools\Anaconda2\envs\FPN_TF\DLLs\;D:\devtools\Anaconda2\envs\FPN_TF\Lib\;D:\devtools\Anaconda2\envs\FPN_TF\Lib\site-packages\;
```
```
3. 先设置path
Path=D:\devtools\Anaconda2\envs\FPN_TF\Scripts\;D:\devtools\Anaconda2\envs\FPN_TF\;C:\Program Files (x86)\Common Files\Oracle\Java\javapath;C:\ProgramData\Oracle\Java\javapath;C:\Windows\system32;C:\Windows;C:\Windows\System32\Wbem;C:\Windows\System32\WindowsPowerShell\v1.0\;C:\Program Files (x86)\NVIDIA Corporation\PhysX\Common;%JAVA_HOME%/bin;%JAVA_HOME%/jre/bin;D:\Program Files\TortoiseSVN\bin;D:\Program Files\VisualSVN Server\bin;C:\Program Files (x86)\Windows Kits\8.1\Windows Performance Toolkit\;C:\Program Files\Microsoft SQL Server\110\Tools\Binn\;C:\Program Files\Git\cmd
这样可以
```
