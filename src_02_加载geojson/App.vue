<template>
  <div id="cesiumContainer"></div>
  <div id="credit"></div>
</template>

<script setup>
import * as Cesium from "cesium";
import { onMounted } from "vue";

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