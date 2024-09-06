## 根据两点计算欧拉角

```js
// 获取欧拉角/姿态角
function getHeadingPitchRoll(pointA, pointB) {
  // 建立以点A为原点，X轴为east,Y轴为north,Z轴朝上的坐标系
  let transform = Cesium.Transforms.eastNorthUpToFixedFrame(pointA)
  //向量AB
  let positionvector = Cesium.Cartesian3.subtract(pointB, pointA, new Cesium.Cartesian3())
  // 因transform是将A为原点的eastNorthUp坐标系中的点转换到世界坐标系的矩阵
  // AB为世界坐标中的向量
  // 因此将AB向量转换为A原点坐标系中的向量，需乘以transform的逆矩阵。
  let vector = Cesium.Matrix4.multiplyByPointAsVector(Cesium.Matrix4.inverse(transform, new Cesium.Matrix4()), positionvector, new Cesium.Cartesian3())
  // 归一化
  let direction = Cesium.Cartesian3.normalize(vector, new Cesium.Cartesian3())
  // heading
  let heading = Math.atan2(direction.y, direction.x) - Cesium.Math.PI_OVER_TWO
  let h = Cesium.Math.TWO_PI - Cesium.Math.zeroToTwoPi(heading)
  let transfrom = Cesium.Transforms.eastNorthUpToFixedFrame(pointA)
  vector = Cesium.Cartesian3.subtract(pointB, pointA, new Cesium.Cartesian3())
  let dir = Cesium.Matrix4.multiplyByPointAsVector(Cesium.Matrix4.inverse(transfrom, transfrom), vector, vector)
  Cesium.Cartesian3.normalize(dir, dir)
  // 因为direction已归一化，斜边长度等于1，所以余弦函数等于direction.z
  let p = Cesium.Math.PI_OVER_TWO - Cesium.Math.acosClamped(dir.z)
  let hpr = new Cesium.HeadingPitchRoll(h, p, 0)
  return hpr
}
```