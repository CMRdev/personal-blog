## Candlestick

- 数据必须包含：时间戳、开盘价、收盘价、最高价格、最低价格
- 当你需要在时间轴上同时看到"从哪来、到哪去、波动多大"时，candlestick 是最高效的选择。

- 核心优势
  - 信息密度高 — 一根蜡烛 = 4 个数值（open, close, high, low）
  - 趋势 + 波动一体化 — 实体方向看趋势，影线长度看波动
  - 异常检测直观 — 长影线或异常实体可快速定位设备异常时段
  - 与时序数据库契合 — SELECT FIRST(val), LAST(val), MAX(val), MIN(val) FROM ... INTERVAL(...) 直出 candlestick 数据

- 示例：

```sql
-- TDengine 查询
SELECT _wstart AS ts, FIRST(temperature) AS open, LAST(temperature) AS close,
       MAX(temperature) AS high, MIN(temperature) AS low
FROM sensor_data
WHERE ts >= '2026-05-12' AND ts < '2026-05-13'
INTERVAL(1h);
```

```js
// ECharts candlestick 配置
option = {
  xAxis: { type: 'category', data: timestamps },
  yAxis: { type: 'value' },
  series: [
    {
      type: 'candlestick',
      data: data.map((d) => [d.open, d.close, d.low, d.high])
    }
  ]
}
```
