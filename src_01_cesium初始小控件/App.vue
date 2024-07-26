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
    animation: false, // 左下动画控件
    timeline: false, // 时间轴控件
    geocoder: false,  // 右上搜索按钮
    homeButton: false, // 右上主页按钮
    navigationHelpButton: false, // 右上帮助按钮
    sceneModePicker: false, // 右上模式选择按钮
    baseLayerPicker: false, // 右上图层选择按钮
    fullscreenButton: false,  // 右下全屏按钮 
  })
  window.viewer = viewer // 方便浏览器控制台打印一些属性

  // viewer._bottomContainer.style.display = "none"
  // viewer._toolbar.style.display = "none"
  // viewer._timeline.container.style.display = "none"
  // viewer._animation._container.style.display = "none"

  viewer.scene.debugShowFramesPerSecond = true; // 显示帧速率控件

})

</script>
<style>
#cesiumContainer {
  height: 100vh;
  width: 100vw;
  overflow: hidden;
}


.cesium-viewer-timelineContainer,
.cesium-viewer-animationContainer,
.cesium-viewer-bottom,
.cesium-viewer-toolbar {
  display: none;
}

/* 全屏按钮 */
.cesium-viewer-fullscreenContainer {
  position: absolute;
  top: -999em;
}
</style>