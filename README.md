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

######Panning Inertia Options
|Option  |Type    |Default |Description|
|--------|--------|--------|-----------|
|inertia |Boolean |*   |If enabled, panning of the map will have an inertia effect where the map builds momentum while dragging and continues moving in the same direction for some time. Feels especially nice on touch devices. Enabled by default unless running on old Android devices.|
|inertiaDeceleration |Number  |3000    |The rate with which the inertial movement slows down, in pixels/second².|
|inertiaMaxSpeed |Number  |Infinity    |Max speed of the inertial movement, in pixels/second.|
|easeLinearity   |Number  |0.2 | |
|worldCopyJump   |Boolean |false   |With this option enabled, the map tracks when you pan to another "copy" of the world and seamlessly jumps to the original one so that all overlays like markers and vector layers are still visible.|
|maxBoundsViscosity  |Number  |0.0 |If maxBounds is set, this option will control how solid the bounds are when dragging the map around. The default value of 0.0 allows the user to drag outside the bounds at normal speed, higher values will slow down map dragging outside bounds, and 1.0 makes the bounds fully solid, preventing the user from dragging outside the bounds.|

######键盘导航参数
|Option  |Type    |Default |Description|
|--------|--------|--------|-----------|
|keyboard    |Boolean |true    |允许用户使用键盘和+ —键来使地图获得焦点和导航|
|keyboardPanDelta    |Number  |80  |当按压箭头键（+、-）移动多少像素|

######鼠标滚轮参数
|Option  |Type    |Default |Description|
|--------|--------|--------|-----------|
|scrollWheelZoom |Boolean或String  |true    |地图是否可以使用鼠标滚轮来缩放。如果传递'center'参数，将会以窗口视图来缩放，而不是鼠标的位置。|
|wheelDebounceTime   |Number  |40  |Limits the rate at which a wheel can fire (in milliseconds). By default user can't zoom via wheel more often than once per 40 ms|
|wheelPxPerZoomLevel |Number  |60  |How many scroll pixels (as reported by L.DomEvent.getWheelDelta) mean a change of one full zoom level. Smaller values will make wheel-zooming faster (and vice versa).|

######触屏交互参数
|Option  |Type    |Default |Description|
|--------|--------|--------|-----------|
|tap |Boolean |true    |使支持移动端(ios,adnroid)的 instant taps和touch holds(Z这个在手机的时候触发事件到事件执行的200MS延迟)|
|tapTolerance    |Number  |15  |The max number of pixels a user can shift his finger during touch for it to be considered a valid tap.|
|touchZoom   |Boolean或String  |*   |是否允许使用两手指拖拽缩放地图。如果传递参数'center'，将会以窗口视图中心进行缩放，而不是手指的位置。对可以触屏操作的web浏览器有效，除了老旧的Android设备|
|bounceAtZoomLimits  |Boolean |true    |如果你不想让地图缩放超过最大最小缩放限制和反弹回来，设置为false|

###Events

######Layer events 图层事件
|Event   |Data    |Description|
|--------|--------|-----------|
|baselayerchange     |[LayersControlEvent](http://leafletjs.com/reference-1.2.0.html#layerscontrolevent)  |当基础图层通过图层控制器[layer control](http://leafletjs.com/reference-1.2.0.html#control-layers)变化时触发.|
|overlayadd  |[LayersControlEvent](http://leafletjs.com/reference-1.2.0.html#layerscontrolevent)  |当覆盖图层通过图层控制器[layer control](http://leafletjs.com/reference-1.2.0.html#control-layers)选中时触发.|
|overlayremove   |[LayersControlEvent](http://leafletjs.com/reference-1.2.0.html#layerscontrolevent)  |当覆盖图层通过图层控制器[layer control](http://leafletjs.com/reference-1.2.0.html#control-layers)弃选时触发.|
|layeradd    |[LayerEvent](http://leafletjs.com/reference-1.2.0.html#layerevent)  |当一个新图层被添加到地图上时触发.|
|layerremove     |[LayerEvent](http://leafletjs.com/reference-1.2.0.html#layerevent)  |当有一些图层从地图上移除时触发|

######Map state change events 地图状态变换事件
|Event   |Data    |Description|
|--------|--------|-----------|
|zoomlevelschange    |[Event](http://leafletjs.com/reference-1.2.0.html#event)   |当由于增加或删除图层引起的缩放级别变换时触发.|
|resize  |[ResizeEvent](http://leafletjs.com/reference-1.2.0.html#resizeevent) |当地图大小发生改变时触发|
|unload  |[Event](http://leafletjs.com/reference-1.2.0.html#event)   |Fired 当地图用[remove](http://leafletjs.com/reference-1.2.0.html#map-remove)方法销毁时触发.|
|viewreset   |[Event](http://leafletjs.com/reference-1.2.0.html#event)   |当地图由于缩放或者下载需要重绘时触发。在创建自定义图层非常有用。|
|load    |[Event](http://leafletjs.com/reference-1.2.0.html#event)   |当地图被初始化时触发（它的中心点和缩放级别第一次被设置时）.|
|zoomstart   |[Event](http://leafletjs.com/reference-1.2.0.html#event)   |当地图缩放级别将要发生变化时触发（缩放动画开始之前）.|
|movestart   |[Event](http://leafletjs.com/reference-1.2.0.html#event)   |当地图窗口视图开始变化时触发（用户开始拖拽地图）.|
|zoom    |[Event](http://leafletjs.com/reference-1.2.0.html#event)   |Fired repeatedly during any change in zoom level, including zoom and fly animations..|
|move    |[Event](http://leafletjs.com/reference-1.2.0.html#event)   |Fired repeatedly during any change in zoom level, including zoom and fly animations..|
|zoomend     |[Event](http://leafletjs.com/reference-1.2.0.html#event)   |当地图已经变化完成时触发（在动画结束之后）.|
|moveend     |[Event](http://leafletjs.com/reference-1.2.0.html#event)   |当地图中心停止变化时触发 (用户停止拖拽地图).|

######Popup events 标记点事件
|Event   |Data    |Description|
|--------|--------|-----------|
|popupopen   |[PopupEvent](http://leafletjs.com/reference-1.2.0.html#popupevent)  |当标记在地图上被打开时触发|
|popupclose  |[PopupEvent](http://leafletjs.com/reference-1.2.0.html#popupevent)  |当标记在地图上被打开时触发|
|autopanstart    |[Event](http://leafletjs.com/reference-1.2.0.html#event)   |当地图开始移动同时标记正在处于opening状态时触发|

######Tooltip events 工具栏事件
|Event   |Data    |Description|
|--------|--------|-----------|
|tooltipopen     |[TooltipEvent](http://leafletjs.com/reference-1.2.0.html#tooltipevent)    |当工具栏在地图上被打开时触发|
|tooltipclose    |[TooltipEvent](http://leafletjs.com/reference-1.2.0.html#tooltipevent)    |当工具栏在地图上被关闭时触发|

######Location events 位置事件
|Event   |Data    |Description|
|--------|--------|-----------|
|locationerror   |[ErrorEvent](http://leafletjs.com/reference-1.2.0.html#errorevent)  |当调用 geolocation 失败时触发 (using the [locate](http://leafletjs.com/reference-1.2.0.html#map-locate) method)|
|locationfound   |[LocationEvent](http://leafletjs.com/reference-1.2.0.html#locationevent)   |当调用 geolocation 成功时触发 (using the [locate](http://leafletjs.com/reference-1.2.0.html#map-locate) method)|

######Interaction events 交互事件
|Event   |Data    |Description|
|--------|--------|-----------|
|click   |[MouseEvent](http://leafletjs.com/reference-1.2.0.html#mouseevent)  |当用户点击或者触拍(移动端)时触发|
|dblclick    |[MouseEvent](http://leafletjs.com/reference-1.2.0.html#mouseevent)  |当用户双击或者双触拍(移动端)时触发|
|mousedown   |[MouseEvent](http://leafletjs.com/reference-1.2.0.html#mouseevent)  |当用户按下鼠标时出发(未释放)|
|mouseup     |[MouseEvent](http://leafletjs.com/reference-1.2.0.html#mouseevent)  |当用户释放鼠标时触发|
|mouseover   |[MouseEvent](http://leafletjs.com/reference-1.2.0.html#mouseevent)  |当鼠标滑进地图时触发|
|mouseout    |[MouseEvent](http://leafletjs.com/reference-1.2.0.html#mouseevent)  |当鼠标滑出鼠标时触发|
|mousemove   |[MouseEvent](http://leafletjs.com/reference-1.2.0.html#mouseevent)  |Fired while the mouse moves over the map.|
|contextmenu |[MouseEvent](http://leafletjs.com/reference-1.2.0.html#mouseevent)  |当用户按下鼠标右键时触发。如果有监听这个事件将会阻止浏览器默认的右键菜单。同时在移动端当用户一只手按住另一只按下时也会触发(也叫长按)|
|keypress    |[KeyboardEvent](http://leafletjs.com/reference-1.2.0.html#keyboardevent)   |当用户按下键盘同时地图正在获得焦点时将会触发|
|preclick    |[MouseEvent](http://leafletjs.com/reference-1.2.0.html#mouseevent)  |当用户点击地图时触发 (sometimes useful when you want something to happen on click before any existing click handlers start running).|

######Other Methods(这里应该是其他事件)
|Event   |Data    |Description|
|--------|--------|-----------|
|zoomanim    |[ZoomAnimEvent](http://leafletjs.com/reference-1.2.0.html#zoomanimevent)   |缩放动画每一帧触发|

###Methods 方法
|Method  |Returns |Description|
|--------|--------|-----------|
|getRenderer(<Path> layer)   |Renderer|    
Returns the instance of Renderer that should be used to render the given Path. It will ensure that the renderer options of the map and paths are respected, and that the renderers do exist on the map.|

######Methods for Layers and Controls 图层和控制器（部件）方法
|Method  |Returns |Description|
|--------|--------|-----------|
|addControl(<Control> control)   |this    |Adds the given control to the map|
|removeControl(<Control> control)    |this    |Removes the given control from the map|
|addLayer(<Layer> layer) |this    |Adds the given layer to the map|
|removeLayer(<Layer> layer)  |this    |Removes the given layer from the map.|
|hasLayer(<Layer> layer) |Boolean |Returns true if the given layer is currently added to the map|
|eachLayer(<Function> fn, <Object> context?) |this    |Iterates over the layers of the map, optionally specifying context of the iterator function.|
|openPopup(<String|HTMLElement> content, <LatLng> latlng, <Popup options> options?) |this    |Creates a popup with the specified content and options and opens it in the given point on a map.|
|closePopup(<Popup> popup?)  |this    |Closes the popup previously opened with openPopup (or the given one).|
|openTooltip(<Tooltip> tooltip)  |this    |Opens the specified tooltip.|
|openTooltip(<String|HTMLElement> content, <LatLng> latlng, <Tooltip options> options?) this    |Creates a tooltip with the specified content and options and open it.|
|closeTooltip(<Tooltip> tooltip?)    |this    |Closes the tooltip given as parameter.|
|openPopup(<Popup> popup)    |this |Opens the specified popup while closing the previously opened (to make sure only one is opened at one time for usability).|

######Methods for modifying map state
|Method  |Returns |Description|
|--------|--------|-----------|
|setView(<LatLng> center, <Number> zoom, <Zoom/pan options> options?)    |this    |Sets the view of the map (geographical center and zoom) with the given animation options.|
|setZoom(<Number> zoom, <Zoom/pan options> options?) |this    |Sets the zoom of the map.|
|zoomIn(<Number> delta?, <Zoom options> options?)    |this    |Increases the zoom of the map by delta (zoomDelta by default).|
|zoomOut(<Number> delta?, <Zoom options> options?)   |this    |Decreases the zoom of the map by delta (zoomDelta by default).|
|setZoomAround(<LatLng> latlng, <Number> zoom, <Zoom options> options)  |this    |Zooms the map while keeping a specified geographical point on the map stationary (e.g. used internally for scroll zoom and double-click zoom).
|setZoomAround(<Point> offset, <Number> zoom, <Zoom options> options)  |this    |Zooms the map while keeping a specified pixel on the map (relative to the top-left corner) stationary.|
|fitBounds(<LatLngBounds> bounds, <fitBounds options> options?)  |this    |Sets a map view that contains the given geographical bounds with the maximum zoom level possible.|
|fitWorld(<fitBounds options> options?)  |this    |Sets a map view that mostly contains the whole world with the maximum zoom level possible.|
|panTo(<LatLng> latlng, <Pan options> options?)  |this    |Pans the map to a given center.|
|panBy(<Point> offset, <Pan options> options?)   |this    |Pans the map by a given number of pixels (animated).|
|flyTo(<LatLng> latlng, <Number> zoom?, <Zoom/pan options> options?)|this |   Sets the view of the map (geographical center and zoom) performing a smooth pan-zoom animation.|
|flyToBounds(<LatLngBounds> bounds, <fitBounds options> options?)    |this   | Sets the view of the map with a smooth animation like flyTo, but takes a bounds parameter like fitBounds.|
|setMaxBounds(<Bounds> bounds)   |this    |Restricts the map view to the given bounds (see the maxBounds option).|
|setMinZoom(<Number> zoom)   |this    |Sets the lower limit for the available zoom levels (see the minZoom option).|
|setMaxZoom(<Number> zoom)   |this    |Sets the upper limit for the available zoom levels (see the maxZoom option).|
|panInsideBounds(<LatLngBounds> bounds, <Pan options> options?)  |this    |Pans the map to the closest view that would lie inside the given bounds (if it's not already), controlling the animation using the options specific, if any.|
|invalidateSize(<Zoom/Pan options> options)  |this    |Checks if the map container size changed and updates the map if so — call it after you've changed the map size dynamically, also animating pan by default. If options.pan is false, panning will not occur. If options.debounceMoveend is true, it will delay moveend event so that it doesn't happen often even if the method is called many times in a row.|
|invalidateSize(<Boolean> animate)   |this |   Checks if the map container size changed and updates the map if so — call it after you've changed the map size dynamically, also animating pan by default.|
|stop()  |this    |Stops the currently running panTo or flyTo animation, if any.|