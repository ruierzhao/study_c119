<template>
  <div id="cesiumContainer"></div>
  <div id="credit"></div>
</template>

<script setup>
import * as Cesium from "cesium";
import { onMounted } from "vue";

Cesium.Ion.defaultAccessToken = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiI5MGI4MGIyYi02YTkyLTQ2MmQtYmU1NC0xZDA4NDhjMmNhNWEiLCJpZCI6MjA4NDIyLCJpYXQiOjE3MTI5ODA0MzB9.EyfN0dxYCL5zgu8L3bFia69viTZYF89sBFJG_WpGrs0"


onMounted(() => {
  const viewer = new Cesium.Viewer("cesiumContainer", {
    infoBox: false
  });
  Cesium.GeoJsonDataSource.load("/src/testdata.json").then((res) => viewer.dataSources.add(res).then((res) => viewer.zoomTo(res)))

  viewer.entities.add({
    position: Cesium.Cartesian3.fromDegrees(116.5, 39),
    point: {
      pixelSize: 20
    }
  })
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