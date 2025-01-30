---
title: "GoogleMapAPI－基本載入"
seoTitle: "GoogleMapAPI－基本載入"
seoDescription: "google map api 新手教學，請安心服用。"
datePublished: Thu Apr 14 2016 00:00:00 GMT+0000 (Coordinated Universal Time)
cuid: cm6jbehcg000h0ajx8lnr90zd
slug: googlemapapi
tags: map

---

google map api 新手教學，請安心服用。

本篇系列紀錄為 [w3cgoogleapi](http://www.w3schools.com/googleapi/default.asp) 上的學習心得記錄，

google map 很好用，真的要學起來～

Using API
---------

```html
<script src="http://maps.googleapis.com/maps/api/js"></script>
```

Initialize 
-----------

```javascript
function initialize(){
}
```

Set Map
-------

```javascript
var mapProp = {
  center:new google.maps.LatLng(24.1504536, 120.6810641),
  zoom: 17,
  mapTypeId: google.maps.MapTypeId.ROADMAP
};
```

mapTypeId：

*      ROADMAP (normal, default 2D map)
*      SATELLITE (photographic map)
*      HYBRID (photographic map + roads and city names)
*      TERRAIN (map with mountains, rivers, etc.)

  
Create Map
-------------

在 initialize() 內，建立地圖物件，將剛剛參數指定進去。

```javascript
var map = new google.maps.Map(document.getElemtentById("googleMap"), mapProp );
```

   
Map Container
-----------------

```html
<div id="googleMap" style="width:500px;height:380px;"></div>
```

Add an Event
------------

加在js檔案中，建立事件頃聽

```javascript
google.map.event.addDomListener(window, 'load', initianlize);
```

以上即完成地圖基本載入

Asynchronously Loading
----------------------

此方法為將 initialize() 參數轉為 parameter 帶入 url。  
於 callback 後串接 function：

```javascript
function loadScript(){
  var script = document.createElement("script");
  script.src = "http://maps.googleapis.com/maps/api/js?callback=initialize";
  document.body.appendChild(script);
}

window.onload = loadScript;
```

Map Demo  
[CodePen](http://codepen.io/ta7382/pen/ZOaWjG)  
 

有勘誤之處，不吝指教。ob'\_'ov