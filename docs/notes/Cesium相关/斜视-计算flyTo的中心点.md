# 斜视 angle-计算 flyTo 的中心点

- 当想要倾斜定位到某个目标点位时，目标会脱离相机的可视范围，此时需要重新计算相机 camera 的位置，以保证可观测到目标点

## 1、直接上代码

```js
function viewControl(angle = -50) {
  let [lon, lat, height] = [123.0, 30.0, 1000]
  const entity = new Cesium.Entity({
    id: `view-control`,
    position: Cesium.Cartesian3.fromDegrees(lon, lat, 0),
    model: {
      show: true,
      uri: './assets/model/warrior.glb',
      scale: 1,
      minimumPixelSize: 128, // 模型的最小像素大小，而不考虑缩放
      distanceDisplayCondition: new Cesium.DistanceDisplayCondition(0.0, 4e8)
    }
  })
  dataSource.entities.add(entity)
  let processedLat = getOffsetLat({ lat: lat, pitch: angle, height: height })
  viewer.camera.flyTo({
    destination: Cesium.Cartesian3.fromDegrees(lon, processedLat, height),
    orientation: {
      heading: Cesium.Math.toRadians(0.0),
      pitch: Cesium.Math.toRadians(angle),
      roll: Cesium.Math.toRadians(0.0)
    }
  })
  // 计算纬度偏移
  function getOffsetLat(options) {
    const { lat, pitch, height } = options
    const ONE_LAT_TO_METERS = 111 * 1000 // 一纬度对应距离111km
    if (Math.abs(pitch % 90) == 0) {
      // 0度和90度不做处理
      return lat
    }
    const latOffsetMeters = height / Math.tan((pitch * Math.PI) / 180) // tan是弧度，（将角度转为弧度）
    const lat_height = Number((latOffsetMeters / ONE_LAT_TO_METERS).toFixed(12))
    return lat + lat_height
  }
}
```
