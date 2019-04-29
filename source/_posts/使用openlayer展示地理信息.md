---
title: 使用openlayers
date: 2019-03-15 15:15:07
categories:
  - openlayers
tags:
---

## 使用openlayers在网页中展示地理信息
### 1.  介绍
--------
这里涉及到几个基础的概念，View, Layer, Control, Interaction, Overlay, Source, Projection 这些对象一起构成了Map
#### 1.1 View
View管理Map的视图参数，缩放zoom, 偏转rotation, 分辨率resolution, 视图中心center等，也可以对这些参数设置范围，从而实现对视图显示的控制
#### 1.2 Layer
Layer是Map显示的基本单位，layer从自身的Source获取数据病将其显示在Map上，一个Map可以包含多个Layer，可以将这些Layer的数据同时显示在Map上，从而实现一个各种地理信息的显示

> 上层的Layer会遮盖下层的Layer

* ###### Source
    指定layer的数据来源
#### 1.3 Control
openlayers自身包含了一些内置的Map控件，像全屏，定位，旋转的按钮，通过控件可以实现以Map的交互，也可以自定义实现需要功能的控件，实现业务需要的交互效果
#### 1.4 Interaction
openlayers默认包含了拖拽，点击等常用的交互行为，如果要定制复杂的交互，可以自定义并注册到Map中就可以实现
#### 1.5 Overlay
高组件可以将dom节点与地图坐标系位置绑定，将dom显示在绑定的地理坐标，该dom将被openlayer控制显示


![](https://user-gold-cdn.xitu.io/2019/4/29/16a6845c80fc8142?w=1461&h=1001&f=png&s=129464)

### 2. 实践
-------
实现一个简单的Map
        
    // 创建贴图层显示底图，这里使用本地的WMS服务
    var imageLayer = new ol.layer.Image({
        source: new ol.source.ImageWMS({
            params: {
                LAYERS: '_all_', // 图层名称
                FORMAT: 'image/png', // 图片格式
                VERSION: '1.1.1' // 服务版本号
            },
            projection: 'EPSG3857', //投影坐标系
            url: URL // WMS地址
        });
    });
    // 创建一个矢量图层，显示一些矢量数据
    var vectorLayer = new ol.source.Vector({
        format: new ol.format.GeoJSON(),
        style: styleInstance //设置矢量数据的显示样式
    });
    // 创建View，设置视图
    var view = new ol.View({
        center: [75, 30], //当前投影坐标系下中心点的坐标
        zoom: 15 //缩放等级
    });
    var map = new ol.Map({
        target: 'map_container', // 将地图挂在到id为map_container的dom上
        view: view,
        layers: [// 图层顺序与列表顺序相反
            imageLayer,
            vectorLayer
        ]
    });