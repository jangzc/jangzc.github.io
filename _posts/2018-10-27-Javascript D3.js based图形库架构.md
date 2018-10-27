---
layout:     post
title:      d3.js based图形库架构
subtitle:   javascript
date:       2018-10-18
author:     Jang
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - Javascript
    - D3
    - 数据可视化
---

# 1. What I'm building?
* Build chart <span style="color:bule">A</span>
* Build chart <span style="color:bule">A</span> again
* Build chart <span style="color:bule">A</span> but make it look different(Style/layout)
* Build chart <span style="color:bule">A</span> but add functionality <span style="color:green">B</span>
* Build chart <span style="color:bule">A</span> with functionality <span style="color:green">B</span> and functionality <span style="color:red">C</span>
* For mobile use chart <span style="color:bule">A</span>, but not functionalities <span style="color:green">B</span> or <span style="color:red">C</span>
* For tablet use chart <span style="color:bule">A</span> with functionalities <span style="color:green">B</span>, but no <span style="color:red">C</span>
* Now build A2 that's like <span style="color:bule">A</span> but differnrt...

# 2. What does it need to do?
* It has to manage a bunch of containers(g/div/etc)
* It renders data(obviously)
* It redraws or may need to redraw in the feature
* It has scales(x,y,colors etc)
* It needs dimensions (height, width, margin)
* It needs to know what device it's on (mobile, web, tablet)
* It uses some visaul marks, often many types for the same data
* It needs to capture users interactions and possibly react

# 3. How we build it?
* Dimensions (height/width/margins)
* Scales （range & domain defined separately)
* Some containers
* Calculations that happen because data is aviilable
* A data bunding
* Ente/update/exit selections & respctive transition selections

# 4. What is a reuseable chart?
* Repeatable: Easy to create multiple instances of
* Configurable: Easy to appropriate for a specific task
* Extensible: Easy to extend with additional functionality
* Composable: Easy to combine into other charts
