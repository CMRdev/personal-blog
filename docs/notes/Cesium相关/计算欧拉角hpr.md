## 根据两点计算欧拉角

- 由 pointA 指向 pointB
- 参数 pointA、pointB 均为笛卡尔坐标 Cartesian3

```js
// 获取欧拉角(只计算heading、pitch)
function getHeadingPitchRoll(pointA, pointB) {
  // 建立以A为原点，x轴为east，y轴为north，z轴朝上的坐标系（transform->四元组）
  const transform = Cesium.Transforms.eastNorthUpToFixedFrame(pointA)
  // 向量AB：subtract-计算差值（B - A = AB）
  const vector_AB = Cesium.Cartesian3.subtract(pointB, pointA, new Cesium.Cartesian3())
  // transform是将[以A为原点的东北上坐标系中的点]转换为世界坐标系所用到的矩阵
  // AB为世界坐标系中的向量
  // 因此，将AB向量转换为以A为原点的坐标系中的向量，需要乘以transform的逆矩阵（站心坐标系）
  const vector_AB_station = Cesium.Matrix4.multiplyByPointAsVector(Cesium.Matrix4.inverse(transform, new Cesium.Matrix4()), vector_AB, new Cesium.Cartesian3())
  // 归一化
  const vector_normalize = Cesium.Cartesian3.normalize(vector_AB_station, new Cesium.Cartesian3())
  // heading: atan2(y,x) -> 将x轴旋转到目标点扫过的角度（当y为正号时逆时针旋转，当y为负号时顺时针旋转）
  const h = Math.atan2(vector_normalize.y, vector_normalize.x)
  const heading = Cesium.Math.TWO_PI - Cesium.Math.zeroToTwoPi(h) // 将值h映射到[0, 2Pi]之间
  // pitch：因为vector_normalize已经归一化，斜边长为1，所以余弦函数等于vector_normalize.z
  // acos -> 将z值转换为弧度；acosClamped -> 将z值限定在[-1, 1]范围内再转为弧度
  const pitch = Cesium.Math.PI_OVER_TWO - Cesium.Math.acosClamped(vector_normalize.z)
  return new Cesium.HeadingPitchRoll(heading, pitch, 0)
}
```

```js
// 获取欧拉角
function getHeadingPitchRoll(pointA, pointB) {
  // 向量AB：subtract-计算差值（B - A = AB）
  const vector_AB = Cesium.Cartesian3.subtract(pointB, pointA, new Cesium.Cartesian3())
  // 归一化
  const vector_normalize = Cesium.Cartesian3.normalize(vector_AB, new Cesium.Cartesian3())
  // 将位置和速度转换为旋转矩阵
  const rotationMatrix3 = Cesium.Transforms.rotationMatrixFromPositionVelocity(pointB, vector_normalize, Cesium.Ellipsoid.WGS84)
  // 从表示旋转的 Matrix3 和表示平移的 Cartesian3 计算 Matrix4 实例
  const modelMatrix4 = Cesium.Matrix4.fromRotationTranslation(rotationMatrix3, pointB)
  // 假设矩阵是仿射变换矩阵，获取所提供矩阵的平移部分
  // const C3 = Cesium.Matrix4.getTranslation(modelMatrix4, new Cesium.Cartesian3()) // 这个C3其实等于pointB
  // 建立以pointB为原点，x轴为east，y轴为north，z轴朝上的坐标系（transform->四元组）
  const transform = Cesium.Transforms.eastNorthUpToFixedFrame(pointB, Cesium.Ellipsoid.WGS84, new Cesium.Matrix4())
  // 计算两个矩阵的乘积
  const m4 = Cesium.Matrix4.multiply(Cesium.Matrix4.inverse(transform, new Cesium.Matrix4()), modelMatrix4, new Cesium.Matrix4())
  // 得到旋转矩阵
  const m3 = Cesium.Matrix4.getMatrix3(m4, new Cesium.Matrix3())
  // 计算四元数
  const q = Cesium.Quaternion.fromRotationMatrix(m3)
  // 计算旋转角(弧度)
  const hpr = Cesium.HeadingPitchRoll.fromQuaternion(q)
  return hpr
}
```
