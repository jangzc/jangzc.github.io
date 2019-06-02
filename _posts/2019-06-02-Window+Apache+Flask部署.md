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


## 1. Eclipse环境(Maven)
### 1.1. 安装jee
### 1.2. 配置maven settings.xml
```
<?xml version="1.0" encoding="UTF-8"?>
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 http://maven.apache.org/xsd/settings-1.0.0.xsd">
    <localRepository>D:/devtool/smavenrepo</localRepository>

    <proxies>
        <proxy>
            <id>http</id>
            <active>true</active>
            <protocol>http</protocol>
            <username>id</username>
            <password>pw</password>
            <host>109.123.97.11</host>
            <port>8080</port>
            <nonProxyHosts>182.192.69.162</nonProxyHosts>
        </proxy>
        <proxy>
            <id>https</id>
            <active>true</active>
            <username>username</username>
            <password>passwd</password>
            <host>109.123.97.11</host>
            <port>8080</port>
            <nonProxyHosts>182.192.69.162</nonProxyHosts>
        </proxy>
    </proxies>

    <mirrors>
        <mirror>
            <id>alimaven</id>
            <mirrorOf>*</mirrorOf>
            <name>aliyun maven</name>
            <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
        </mirror>
    </mirrors>

</settings>
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
