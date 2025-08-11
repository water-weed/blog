---
title: '多边形复杂度系统'

date: 2025-04-30T11:00:00-07:00
lastmod: 2025-04-30T11:00:00-07:00

draft: ture
math: true

categories:
  - 项目集
tags:
  - Vue.js
  - Python
  - 网页应用
  - 计算机图形学
---

## 基本信息
项目类型：网页应用/计算机图形学  
技术栈：前端：vue.js  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;后端：python  
核心功能：输入多边形 / 计算多边形复杂度 / 数据可视化 / 数据导出 / 理论介绍  
访问链接：http://8.211.35.218:5173/ &nbsp;&nbsp;密码：123456  
<!--more-->

## 简介
量化多边形复杂度一直被许多研究领域研究，例如，零件制造，图像处理，模式识别，空间数据库，视觉研究等领域。同时，多边形复杂度也在许多领域有重要的应用，例如作为计算机图形建模的重要参数，帮助分析给定形状的复杂度，以辅助决策并优化图像渲染或零件设计方案。然而，基于不同的认知感受，知识背景和应用，产生了许多不同的多边形复杂度的定义。许多研究者尝试从不同角度和不同理论定义多边形复杂度，如信息论，机器学习，多边形骨架，加权模型等等。

在这个系统中，实现了八种多边形复杂度的计算方法，并实现了三种输入多边形的方式，数据可视化，数据导出等功能。

## 算法实现
- 下采样区域 downsampling area
- 下采样边界 downsampling boundary
- 基于边界的方法 boundary
- 三角剖分 triangulation
- 熵 Entropy
- 中轴变换 Medial Axis Transform（MAT）
- 扩展距离函数 Extended Distance Function （EDF）
- 加权模型：振动频率，振动幅度，偏离凸包的程度 weighted measure: frequency of vibration, amplitude of vibration, deviation from the convex hull

## 系统介绍
该系统主要由Home（首页），System（系统），Theroy（理论）三个页面构成。
### Home（首页）
Home（首页）页面主要介绍了该系统的具体情况和开发背景。以及通过页面的左侧边栏，可以进入其他页面，包括System description（系统描述）页面，System（系统）页面和六个理论子页面。
![Home（首页）](/blog/images/polygon_complexity_system/Home.png)
### System（系统）
该系统包含三个功能：输入多边形图片，结果数据可视化，结果数据导出。有三种方法可以输入图片：选择已有多边形图片，上传多边形图片或者在网页上绘制多边形。

System（系统）的开始界面如图所示，用户可以通过Select（选择），Upload（上传），Draw（绘制）三个按钮选择输入多边形图片的方式。通过Download按钮可以导出已有的结果数据为excel文件。System一开始会初始化两个多边形示例并计算其复杂度作为示例，使用户对于计算出的复杂度结构有一个基本认知，从而引导用户更快熟悉该系统。
![System（系统）开始界面](/blog/images/polygon_complexity_system/system1.png)
#### 输入多边形
为了满足用户不同的可能的需求，该系统具有三种方式输入多边形图片：从预加载的图片中选择，上传多边形图片，在网页上绘制多边形。

选择多边形页面如图所示。在该页面中，我们选择了MPEG-7 Core Experiment CE-Shape-1数据集中的多边形图片进行预加载。该数据集由Moving Picture Experts Group创建，包含70种共计1400张多边形图片，即每种包含20个相似的形状对象。这个数据集包含了大量多边形形状并被广泛应用于形状匹配和形状检索研究中。我们从每个种类中选择了一张多边形图片作为用户的选择对象。用户可以通过点击图片进行选择。用户同样可以一次性选择多张多边形图片进行对比。点击Cancel按钮可以取消所有选择，并回到System页面。点击Ok按钮，可以确认上传所有选择的图片并跳转回System页面并显示计算结果。
![选择界面](/blog/images/polygon_complexity_system/select.png)

上传多边形页面如图所示。在该页面，用户可以上传自己的多边形图片来计算多边形复杂度。用户可以点击框中的加号，从本地上传图片，上传成功后图片会在框中显示。接受的图片格式包括.jpeg, .jpg, .png, .svg, .bmp和.webp，用户同样可以一次性上传多张图片从而比较结果。用户可以一直点击空白框中加号，添加图片，在将图片上传完成后，可以通过Cancel按钮取消所有上传并回到System页面，或者点击Ok按钮确认将所有多边形图片提交，并返回System页面显示所有上传图片的计算结果。
![上传界面](/blog/images/polygon_complexity_system/Upload.png)

绘制多边形页面如图所示。用户可以在框中自由绘制多变形，可以通过Delete last node按钮删除绘制的最后一个几点，或者使用Clear canvas按钮清除绘制的所有图形。使用Cancel按钮可以取消绘制，并不提交返回System页面，使用Ok按钮可以确认绘制的多边形并上传，返回System页面查看计算结果。
![绘制界面](/blog/images/polygon_complexity_system/draw.png)
#### 数据可视化
数据可视化模块在System页面的下半部分。该模块的主体是展示不同多边形运用不同复杂度计算方法计算得到的复杂度的值的表格。通过表格上方的多选栏，可以选择只展示选择了的方法所计算的属性，这能够帮助用户分析和比较特定的计算方法的结果。同时可以通过拖动表头，改变表格中方法排列的顺序，以用户希望的顺序展示结果。
![可视化模块](/blog/images/polygon_complexity_system/data_visualization.png)

同时点击计算的复杂度的值，可以进入每个方法的详细页面，可以看到每个方法计算时的详细信息，如图所示，是Downsamping Boundary方法的详细页面。我们在每个方法展示的信息如下表所示，我们希望该页面能够帮助用户更加深入地了解每个复杂度值的计算过程。
![详细页面](/blog/images/polygon_complexity_system/detailed.png)

|计算方法|详细信息|
|:-------|:-------|
|基于边界的方法 boundary|图片长度 Length， 图片宽度 Width，周长 $L_b$，复杂度 Complexity value|
|下采样区域 downsampling area|采样率 Sampling rate，下采样图形占用像素 Downsampled occupied pixels，原本图形占用像素 Original occupied pixels，复杂度 Complexity value，下采样图形 Downsampling image|
|下采样边界 downsampling boundary|采样率 Sampling rate，下采样图形周长 Downsampled length，原本图形周长 Original length，复杂度 Complexity value，下采样图形 Downsampling image|
|扩展距离函数 EDF|EDF值图像 EDF value image，复杂度 Complexity value|
|熵 Entropy|熵直方图 Histogram，复杂度 Complexity value|
|中轴变换 MAT|MAT值图像 MAT value image，复杂度 Complexity value|
|三角剖分 triangulation|三角剖分图 Triangulation image，复杂度 Complexity value|
|加权模型 weighted|振动频率 Amplitude of the vibration，振动幅度 Frequency of the vibration，偏离凸包的程度 Deviation from the convex hull，复杂度 Complexity value|
#### 数据导出
通过System页面上的download按钮用户可以将数据可视化的表格导出为excel进行保存，如图所示。表格中有多边形的图片和每种方法计算的值。导出的表格中包括的方法为用户在数据可视化模块中选择展示的方法。
![数据导出](/blog/images/polygon_complexity_system/export.png)
### Theory（理论）
在Theory（理论）页面中，总共有六个子页面，分别介绍了下采样方法 Downsamping，基于边界的方法 Boundary，三角剖分方法 Triangulation，基于熵的方法 Entropy，基于骨架的方法 Skeleton 和加权模型 Weighted, 这六个应用在系统中的复杂度计算方法。下图是介绍下采样方法的页面。在每个子页面中，我们都会从方法的定义和实现过程两方面进行阐述，并提供系统生成的计算结果作为例子，使用户能更加便于理解。
![数据导出](/blog/images/polygon_complexity_system/Theory.png)

##  未来计划
- 对复杂多边形的支持：未来的版本将支持计算复杂多边形的复杂度，包括自交多边形和有洞的多边形
- 加入更多的计算方法
- 对复杂度的值进行归一化：我们计划将所有复杂度结果归一化到[0,1]，从而使得不同方法之间对比更加容易
- 加强数据可视化：添加饼图，折线图，雷达图和其他可视化工具，使得结果更加易于理解
- 改善服务器表现：提高服务器带宽，提高响应速度
