# doc-chinese
doc-chinese是翻译知名的开源库成中文的开源项目
##1.Geo-chinese 地理信息相关开源库
leaflet.js 翻译[leaflet-chinese](https://github.com/unionTime/doc-chinese/blob/master/src/leaflet-chinese.md)

#leaflet-chinese
一个面向移动端友好的开源交互式地图js库

##介绍
leaflet是一个面向移动端友好的开源交互式地图js库，体积大小仅仅38kb，但是拥有几乎所有开发者所需要的地图功能。
leaflet以简单、高性能和易用性为原则进行设计。它可以高效地运行在所有主流的桌面平台和移动平台，可以使用大量的[插件](http://leafletjs.com/plugins.html)进行扩展，拥有美观易用的[api文档](http://leafletjs.com/reference-1.2.0.html)和简单可读性强的[源码](https://github.com/Leaflet/Leaflet)（非常欢迎[贡献](https://github.com/Leaflet/Leaflet/blob/master/CONTRIBUTING.md)）
##简单用法
创建一个"map"div，添加我们想要选择的瓦片数据，和一个用一些文字的标记点：
```
var map = L.map('map').setView([51.505, -0.09], 13);

L.tileLayer('http://{s}.tile.osm.org/{z}/{x}/{y}.png', {
    attribution: '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors'
}).addTo(map);

L.marker([51.5, -0.09]).addTo(map)
    .bindPopup('A pretty CSS3 popup.<br> Easily customizable.')
    .openPopup();
```

学习更多关于[快速指南](http://leafletjs.com/examples/quick-start/),查找相关[教材]()，或者直接进入[api文档](http://leafletjs.com/reference-1.2.0.html)。如何你有什么问题，可以先查看[FAQ](https://github.com/Leaflet/Leaflet/blob/master/FAQ.md)
##API文档

###Map
这是API的核心类——用来在页面上创建地图对象(map)和操作它。
######基本例子
```
// initialize the map on the "map" div with a given center and zoom
var map = L.map('map', {
    center: [51.505, -0.09],
    zoom: 13
});
```
######创建（实例化）
|Factory |Description|
|--------|-----------|
|L.map(<String> id, <Map options> options?)  |传递一个div的id实例化一个地图对象，options 是参数对象（同Map options）|
|L.map(<HTMLElement> el, <Map options> options?) |传递一个已经创建好的div对象(HTML element)，options 是参数对象（同Map options）|

######参数
|Option  |Type    |Default |Description|
|--------|--------|--------|-----------|
|preferCanvas|Boolean| false   |是否路径(Paths)应该用Canvas渲染。默认情况下。所有路径都以SVG的形式渲染|

######控制参数
|Option  |Type    |Default |Description|
|--------|--------|--------|-----------|
|attributionControl  |Boolean |true    |是否贡献标志控件被默认添加|
|zoomControl |Boolean |true    |是否缩放控件被默认添加|

######交互参数
|Option  |Type    |Default |Description|
|--------|--------|--------|-----------|
|closePopupOnClick   |Boolean |true  |设置它为false,如果你不想当用户点击地图时关闭标记|
|zoomSnap    |Number  |1   |缩放水平的效果总是它的整倍数，particularly right after a fitBounds() or a pinch-zoom. By default, the zoom level snaps to the nearest integer; lower values (e.g. 0.5 or 0.1) allow for greater granularity. A value of 0 means the zoom level will not be snapped after fitBounds or a pinch-zoom.|
|zoomDelta   |Number  |1   |控制多大的地图缩放水平将会触发地图的变化，（在使用zoomIn(), zoomOut(), 按压 + or - o在键盘上, 或者使用[zoom controls](http://leafletjs.com/reference-1.2.0.html#control-zoom).）Values smaller than 1 (e.g. 0.5) allow for greater granularity.|
|trackResize |Boolean |true    |是否根据浏览器窗口大小自动调整地图大小|
|boxZoom |Boolean |true    |地图是否在鼠标拖拽成矩形的区域内放大，同时按住shift键|
|doubleClickZoom |Boolean或者String  |true    |地图是否在双击时放大，按住shift键双击时缩小。如果传入参数'center'，双击将会以地图视图中心进行缩放，而不管鼠标悬浮在哪里|
|dragging    |Boolean |true    |地图在使用鼠标或者触摸时是否可拖拽|

######地图状态参数
|Option  |Type    |Default |Description|
|--------|--------|--------|-----------|
|crs |CRS |L.CRS.EPSG3857  |参考坐标系统，如果你不熟悉请不要随意的改动它|
|center  |LatLng  |undefined   |初始化地图中心位置（地理位置）|
|zoom    |Number  |undefined   |初始化缩放级别|
|minZoom |Number  |*   |最小缩放级别。如果没有指定并且至少有一个格网图层[GridLayer](http://leafletjs.com/reference-1.2.0.html#gridlayer)或者瓦片图层[TileLayer](http://leafletjs.com/reference-1.2.0.html#tilelayer)在地图上，minZoom参数的最小值将会替代使用|
|maxZoom |Number  |*   |最大缩放级别。如果没有指定并且至少有一个格网图层[GridLayer](http://leafletjs.com/reference-1.2.0.html#gridlayer)或者瓦片图层[TileLayer](http://leafletjs.com/reference-1.2.0.html#tilelayer)在地图上，maxZoom参数的最大值将会替代使用|
|layers  |Layer[] |[]  |初始化添加到地图上的图层数组|
|maxBounds   |LatLngBounds    |null    |当参数被设置时，地图将限制视图在指定的地理区域内，如果用户尝试将地图拖拽到限制的区域外，将会反弹回来。想要手动设置限制范围，可以使用[setMaxBounds](http://leafletjs.com/reference-1.2.0.html#map-setmaxbounds)方法|
|renderer    |Renderer    |*   |默认在地图上渲染矢量图层的方式，默认选择[L.SVG](http://leafletjs.com/reference-1.2.0.html#svg)或者[L.Canvas](http://leafletjs.com/reference-1.2.0.html#canvas)取决于浏览器支持|

######动画参数
|Option  |Type    |Default |Description|
|--------|--------|--------|-----------|
|zoomAnimation   |Boolean |true    |地图缩放动画是否可用。默认在所有支持css# Transitions的浏览器中可用，除了Android|
|zoomAnimationThreshold  |Number  |4   |如果缩放的差值超过了这个值，将不会有缩放动画效果|
|fadeAnimation   |Boolean |true    |淡入淡出动画是否可用。默认在所有支持css# Transitions的浏览器中可用，除了Android|
|markerZoomAnimation |Boolean |true    |标记是否随地图缩放进行缩放。如果设置为false，当超过动画长度时标记点将会消失。默认在所有支持css# Transitions的浏览器中可用，除了Android|
|transform3DLimit    |Number  |2^23    |Defines the maximum size of a CSS translation transform. The default value should not be changed unless a web browser positions layers in the wrong place after doing a large panBy|
