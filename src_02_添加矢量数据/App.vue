<template>
  <div id="cesiumContainer"></div>
  <div id="credit"></div>
</template>

<script setup>
import * as Cesium from "cesium";
import { onMounted } from "vue";

onMounted(() => {
  const viewer = new Cesium.Viewer("cesiumContainer", {
    shouldAnimate: true //动态需要开启
  })
  window.viewer = viewer
  // #### entity
  // const point = new Cesium.Entity({
  //   position: Cesium.Cartesian3.fromDegrees(116, 40),
  //   point: {
  //     pixelSize: 20
  //   }
  // })
  // viewer.entities.add(point)
  // viewer.zoomTo(point)

  // const point = viewer.entities.add({
  //   position: Cesium.Cartesian3.fromDegrees(116.5, 40),
  //   point: {
  //     pixelSize: 20
  //   }
  // })
  // 完整写法
  const point = viewer.entities.add(
    new Cesium.Entity({
      position: Cesium.Cartesian3.fromDegrees(116.5, 40),
      point: new Cesium.PointGraphics({
        pixelSize: 20
      })
    })
  )

  // ## czml
  // var czml = [{
  //   "id": "document",
  //   "name": "box",
  //   "version": "1.0"
  // }, {
  //   "id": "shape2",
  //   "name": "Red box with black outline",
  //   "position": {
  //     "cartographicDegrees": [-107.0, 40.0, 300000.0]
  //   },
  //   "box": {
  //     "dimensions": {
  //       "cartesian": [400000.0, 300000.0, 500000.0]
  //     },
  //     "material": {
  //       "solidColor": {
  //         "color": {
  //           "rgba": [255, 0, 0, 128]
  //         }
  //       }
  //     },
  //     "outline": true,
  //     "outlineColor": {
  //       "rgba": [0, 0, 0, 200]
  //     }
  //   }
  // }];

  // Cesium.CzmlDataSource.load(czml)
  //   .then((res) => {
  //     viewer.dataSources.add(res)
  //       .then(() => {
  //         setTimeout(() => {
  //           viewer.zoomTo(res)
  //         }, 5000)

  //       })
  //   })

  // ## geojson
  var geojson = {
    "type": "FeatureCollection",
    "features": [
      {
        "type": "Feature",
        "properties": {},
        "geometry": {
          "coordinates": [
            [
              [
                116.28413009214364,
                40.09126930439871
              ],
              [
                116.12888873758385,
                40.06670632732545
              ],
              [
                116.10674395599347,
                39.97034992991155
              ],
              [
                116.16831311654528,
                39.76814709175818
              ],
              [
                116.42953771693556,
                39.800336421693515
              ],
              [
                116.59959392057402,
                39.860897215717756
              ],
              [
                116.72035753461711,
                39.9289661601193
              ],
              [
                116.79922046954391,
                40.036603036700996
              ],
              [
                116.72035661147544,
                40.15913929437198
              ],
              [
                116.49357330739451,
                40.183566365375356
              ],
              [
                116.28413009214364,
                40.09126930439871
              ]
            ]
          ],
          "type": "Polygon"
        }
      }
    ]
  }
  // Cesium.GeoJsonDataSource.load(geojson)
  //   .then((res) => {
  //     console.log(res);
  //     viewer.dataSources.add(res)
  //       .then((res) => {
  //         console.log(res);
  //         setTimeout(() => {
  //           viewer.zoomTo(res)
  //         }, 3500)
  //       })
  //   })

  const pinBuilder = new Cesium.PinBuilder();

  Cesium.GpxDataSource.load(
    "src/assets/lamina.gpx",
    {
      clampToGround: true,
      trackColor: Cesium.Color.YELLOW,
      waypointImage: pinBuilder.fromMakiIconId(
        "bicycle",
        Cesium.Color.BLUE,
        48
      ),
    }
  ).then((res) => {
    viewer.dataSources.add(res)
      .then((res) => {
        viewer.zoomTo(res);
      })
  })

  viewer.zoomTo(point)
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
</style>