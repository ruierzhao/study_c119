/// 关闭cesium 自带控件
// 1.使用Viewer constractor
```js
window.viewer = new Cesium.Viewer("cesiumContainer", {
    animation: false, // 左下动画控件
    timeline: false, // 时间轴控件
    geocoder: false,  // 右上搜索按钮
    homeButton: false, // 右上主页按钮
    navigationHelpButton: false, // 右上帮助按钮
    sceneModePicker: false, // 右上模式选择按钮
    baseLayerPicker: false, // 右上图层选择按钮
    fullscreenButton: false,  // 右下全屏按钮 
})
```

// 2.使用css
```css
.cesium-viewer-timelineContainer,
.cesium-viewer-animationContainer,
.cesium-viewer-bottom,
.cesium-viewer-toolbar {
    display: none;
}
.cesium-viewer-fullscreenContainer  /* 全屏按钮 */
{ position: absolute; top: -999em;  }
```

// 3.使用js设置css
```js
viewer._bottomContainer.style.display = "none"
viewer._toolbar.style.display = "none"
viewer._timeline.container.style.display = "none"
viewer._animation._container.style.display = "none"

viewer.scene.debugShowFramesPerSecond = true; // 显示帧速率控件


```
