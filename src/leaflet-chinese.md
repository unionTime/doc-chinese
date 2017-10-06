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
|closePopupOnClick   |Boolean |true    |Set it to false if you don't want popups to close when user clicks the map.|
|zoomSnap    |Number  |1   |Forces the map's zoom level to always be a multiple of this, particularly right after a fitBounds() or a pinch-zoom. By default, the zoom level snaps to the nearest integer; lower values (e.g. 0.5 or 0.1) allow for greater granularity. A value of 0 means the zoom level will not be snapped after fitBounds or a pinch-zoom.|
|zoomDelta   |Number  |1   |Controls how much the map's zoom level will change after a zoomIn(), zoomOut(), pressing + or - on the keyboard, or using the zoom controls. Values smaller than 1 (e.g. 0.5) allow for greater granularity.
|trackResize |Boolean |true    |Whether the map automatically handles browser window resize to update itself.|
|boxZoom |Boolean |true    |Whether the map can be zoomed to a rectangular area specified by dragging the mouse while pressing the shift key.|
|doubleClickZoom |Boolean/|String  |true    |Whether the map can be zoomed in by double clicking on it and zoomed out by double clicking while holding shift. If passed 'center', double-click zoom will zoom to the center of the view regardless of where the mouse was.|
|dragging    |Boolean |true    |Whether the map be draggable with mouse/touch or not.|