<template>
  <div id="cesiumContainer"></div>
</template>

<script setup>
import * as Cesium from "cesium";
import { onMounted } from "vue";

Cesium.Ion.defaultAccessToken = defaultAccessToken

var tdtBaseUrl = "https://{s}.tianditu.gov.cn"
var subdomains = ['t0', 't1', 't2', 't3', 't4', 't5', 't6', 't7'];
var token = TDTkey

// 叠加影像服务
var imgMap = new Cesium.UrlTemplateImageryProvider({
  url: tdtBaseUrl + 'DataServer?T=img_w&x={x}&y={y}&l={z}&tk=' + token,
  subdomains: subdomains,
  tilingScheme: new Cesium.WebMercatorTilingScheme(),
  maximumLevel: 18
});


// 叠加国界服务
var iboMap = new Cesium.UrlTemplateImageryProvider({
  url: tdtBaseUrl + 'DataServer?T=ibo_w&x={x}&y={y}&l={z}&tk=' + token,
  subdomains: subdomains,
  tilingScheme: new Cesium.WebMercatorTilingScheme(),
  maximumLevel: 10
});

var zhuji = new Cesium.WebMapTileServiceImageryProvider({
  url: "http://t0.tianditu.com/cva_w/wmts?service=wmts&request=GetTile&version=1.0.0&LAYER=cva&tileMatrixSet=w&TileMatrix={TileMatrix}&TileRow={TileRow}&TileCol={TileCol}&style=default.jpg&tk=" + token,
  layer: "tdtAnnoLayer",
  style: "default",
  format: "image/jpeg",
  subdomains: subdomains,
  tileMatrixSetID: "GoogleMapsCompatible"
})
// 原文链接：https://blog.csdn.net/Enbir/article/details/122586905
var 矢量底图 = new Cesium.WebMapTileServiceImageryProvider({
  url: "http://t0.tianditu.com/vec_w/wmts?service=wmts&request=GetTile&version=1.0.0&LAYER=vec&tileMatrixSet=w&TileMatrix={TileMatrix}&TileRow={TileRow}&TileCol={TileCol}&style=default&format=tiles&tk=" + token,
  layer: "tdtVecBasicLayer",
  style: "default",
  format: "image/jpeg",
  subdomains: subdomains,
  tileMatrixSetID: "GoogleMapsCompatible",
  show: false
})

// 叠加地形服务
// var terrainUrls = new Array();
// for (var i = 0; i < subdomains.length; i++) {
//   var url = tdtBaseUrl.replace('{s}', subdomains[i]) + 'mapservice/swdx?T=elv_c&tk=' + token;
//   terrainUrls.push(url);
// }
// Cesium.TerrainProvider
// var provider = new Cesium.TerrainProvider({
//   // urls: terrainUrls
//   urls: [].map((item) => {
//     return tdtBaseUrl.replace('{s}', item) + 'mapservice/swdx?T=elv_c&tk=' + token
//   })
// });


onMounted(() => {
  const viewer = new Cesium.Viewer("cesiumContainer")
  window.viewer = viewer

  // viewer.imageryLayers.addImageryProvider(imgMap);
  // viewer.imageryLayers.addImageryProvider(iboMap);
  viewer.imageryLayers.removeAll();
  viewer.imageryLayers.addImageryProvider(矢量底图);
  viewer.imageryLayers.addImageryProvider(zhuji);

})

</script>
<style>
#cesiumContainer {
  height: 100vh;
  width: 100vw;
  overflow: hidden;
}

/* .cesium-viewer-timelineContainer,
.cesium-viewer-animationContainer,
.cesium-viewer-bottom,
.cesium-viewer-toolbar {
  display: none;
} */
</style>