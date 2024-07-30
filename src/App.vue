<template>
  <div id="cesiumContainer"></div>
</template>

<script setup>
import * as Cesium from "cesium";
import { onMounted } from "vue";

Cesium.Ion.defaultAccessToken = defaultAccessToken

onMounted(() => {
  const viewer = new Cesium.Viewer("cesiumContainer")
  window.viewer = viewer

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