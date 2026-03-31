# IDMP Chart 可视化能力提升计划

> 基于现有代码分析，对比 Grafana 配置能力制定。以下功能已由其他方式处理，不列入本计划：
> 单位系统、小数位数（已有其他处理方式）、Reduce 函数（SQL层处理）、Overrides 系统（不需要）、Legend / Data Links / Standard Options（通用组件已实现，所有 chart type 均已支持）。
>
> 工作量估算基于 AI 辅助编程（Claude Code），具体工作模式见第三部分。

---

## 第一部分：现有 Chart Type 配置补全

### 1. Line Chart (Trend)

| 配置项 | 现状 | 待补充说明 |
|--------|:----:|-----------|
| Title / SubTitle | ✅ | |
| Line Style (lines/step/smooth) | ✅ | |
| Step Interpolation | ✅ | |
| Line Type (solid/dashed/dotted) | ✅ | |
| Line Width | ✅ | |
| Line Opacity | ✅ | |
| Fill Opacity | ✅ | |
| Label Rotate / Interval | ✅ | |
| Stack Mode | ✅ | |
| Multi-lane | ✅ | |
| Y轴（左/右，title/min/max） | ✅ | |
| Limits / Thresholds | ✅ | |
| 系列颜色 | ❌ | 每条线独立配色 |
| 显示数据点 | ❌ | auto/never/always + 点大小 |
| Gradient Fill Mode | ❌ | none/opacity/hue/scheme |
| Connect Null Values | ❌ | none/linear/threshold |
| Tooltip 模式 | ❌ | single/all/hidden |
| X轴配置 | ❌ | 显示/隐藏、时间格式 |

---

### 2. Bar Chart

| 配置项 | 现状 | 待补充说明 |
|--------|:----:|-----------|
| Title / SubTitle | ✅ | |
| Orientation | ✅ | |
| Bar Width / Opacity | ✅ | |
| Label Rotate / Interval | ✅ | |
| Stack Mode | ✅ | |
| Y轴 | ✅ | |
| Limits | ✅ | |
| 系列颜色 | ❌ | 每根柱独立配色 |
| 柱上 Value Label | ❌ | 显示/隐藏、位置、字号 |
| Tooltip 模式 | ❌ | single/all/hidden |
| X轴配置 | ❌ | 显示/隐藏、时间格式 |

---

### 3. Pie Chart

| 配置项 | 现状 | 待补充说明 |
|--------|:----:|-----------|
| Title | ✅ | |
| Donut 模式 | ❌ | 内圆半径可调 |
| Slice 颜色 | ❌ | 每个 slice 独立颜色 |
| 标签显示 | ❌ | name/value/percent/组合 |
| 标签位置 | ❌ | inside/outside |
| 排序 | ❌ | 按值升序/降序 |
| Tooltip | ❌ | |
| Stroke | ❌ | 边框宽度、颜色 |

---

### 4. Gauge

| 配置项 | 现状 | 待补充说明 |
|--------|:----:|-----------|
| Title | ✅ | |
| Orientation | ✅ | |
| Display Time | ✅ | |
| Show Threshold Labels | ✅ | |
| Title / Value Font Size | ✅ | |
| 阈值颜色 | ✅ | 已通过通用 Limits 组件实现 |
| Min / Max | ⚠️ | 模型字段已有，UI 和渲染均未接入，需补 |
| Value Mappings | ❌ | |

---

### 5. Stat

| 配置项 | 现状 | 待补充说明 |
|--------|:----:|-----------|
| Orientation | ✅ | |
| Display Time | ✅ | |
| Title / Value 字号、颜色 | ✅ | |
| Background Color | ✅ | |
| Width | ✅ | |
| Text 模式 | ❌ | value/name/value+name |
| Sparkline | ❌ | 背景小折线图 |
| Color 模式 | ❌ | background/value/none |

---

### 6. Table

| 配置项 | 现状 | 待补充说明 |
|--------|:----:|-----------|
| Timestamp Format | ✅ | |
| Column Aliases | ✅ | |
| 列宽 | ❌ | auto / 固定 px |
| 列对齐 | ❌ | left/center/right |
| Cell 类型 | ❌ | 颜色背景、color-text |
| 阈值着色 | ❌ | 按值范围着色 |
| Value Mappings | ❌ | |
| Footer | ❌ | sum/mean/min/max/count |
| 列排序 | ❌ | 默认排序列 |

---

### 7. Map（地图）

| 配置项 | 现状 | 待补充说明 |
|--------|:----:|-----------|
| GeoJSON 文件上传 | ✅ | |
| Visual Map Min/Max | ✅ | |
| 3色渐变 | ✅ | |
| 显示标签 | ✅ | |
| Basemap 类型选择 | ❌ | OpenStreetMap / CARTO / ArcGIS / 自定义 XYZ Tile |
| 初始视图 | ❌ | 经纬度中心点 + 缩放级别 / 自适应数据范围 |
| 地图控件 | ❌ | 缩放按钮、鼠标滚轮缩放、比例尺、归属信息显示 |
| Markers 图层 | ❌ | 点标记，大小/颜色/图标可按数据驱动配置 |
| Heatmap 图层 | ❌ | 热力点叠加，radius/blur/opacity 可配置 |
| 多图层管理 | ❌ | 添加/删除/排序多个图层 |
| 位置模式 | ❌ | 经纬度字段映射 / Geohash / 自动识别字段名 |
| Tooltip 模式 | ❌ | 悬停显示 / 点击显示 / 关闭 |
| GeoJSON 样式规则 | ❌ | 按字段值条件着色，不只是统一渐变 |

---

### 8. Text（富文本）

| 配置项 | 现状 | 待补充说明 |
|--------|:----:|-----------|
| 背景颜色 | ✅ | |
| 背景图片 | ✅ | |
| 背景图片布局（none/cover/repeat） | ✅ | |
| 内容渲染模式 | ❌ | Markdown / HTML / 纯文本，Grafana 三种都支持 |
| 变量插值 | ❌ | 内容中引用 dashboard 变量（Grafana 支持） |

---

### 9. Scatter

| 配置项 | 现状 | 待补充说明 |
|--------|:----:|-----------|
| Title / SubTitle | ✅ | |
| Symbol 类型 / 大小 | ✅ | |
| Opacity | ✅ | |
| Special Points | ✅ | |
| Label Rotate / Interval | ✅ | |
| Y轴 | ✅ | |
| Data Analysis (clustering/regression) | ✅ | |
| 系列颜色 | ❌ | 多系列时每个系列独立配色 |
| Tooltip | ❌ | |

---

### 10. Bar Gauge

| 配置项 | 现状 | 待补充说明 |
|--------|:----:|-----------|
| Title / SubTitle | ✅ | |
| Orientation | ✅ | |
| Display Time | ✅ | |
| Display Mode (gradient/basic/retroLCD) | ✅ | |
| Value Display | ✅ | |
| Name Placement | ✅ | |
| Bar Size (auto/manual, min/max) | ✅ | |
| Color Thresholds | ✅ | |
| Threshold Mode (absolute/percentage) | ✅ | |
| Value Mappings | ❌ | |
| Tooltip | ❌ | |

---

### 11. State Timeline

| 配置项 | 现状 | 待补充说明 |
|--------|:----:|-----------|
| Title / SubTitle | ✅ | |
| Border Width | ✅ | |
| Row Height | ✅ | |
| Fill Opacity | ✅ | |
| Label Rotate / Interval | ✅ | |
| Limits（带颜色阈值） | ✅ | |
| Value Mappings | ❌ | 类似 Status History |
| Tooltip | ❌ | |

---

### 12. Status History

| 配置项 | 现状 | 待补充说明 |
|--------|:----:|-----------|
| Title / SubTitle | ✅ | |
| Value Mappings（5种类型） | ✅ | |
| Border Width | ✅ | |
| Row Height / Column Width | ✅ | |
| Fill Opacity | ✅ | |
| Label Rotate / Interval | ✅ | |
| Tooltip | ❌ | |

---

### 工作量汇总

| 任务 | 涉及 Chart | 工作量 |
|------|-----------|:------:|
| 系列颜色 | Line、Bar、Scatter、Pie | 1天 |
| Pie Chart 全面补全 | Pie | 1天 |
| Gauge 补全（min/max UI接入 + value mapping） | Gauge | 0.5天 |
| Stat 补全（text模式/sparkline/color模式） | Stat | 0.5天 |
| Table 高级配置（列宽/对齐/cell类型/footer/阈值着色） | Table | 2天 |
| Line/Bar 补全（数据点/connect null/value label/X轴） | Line、Bar | 1天 |
| Map 补全（basemap/初始视图/地图控件/markers/位置模式/tooltip） | Map | 5天 |
| Text 补全（渲染模式/变量插值） | Text | 0.5天 |
| Value Mappings 通用化 | Gauge、Bar Gauge、State Timeline、Table | 0.5天 |
| Tooltip 配置 | 所有 chart | 0.5天 |
| 测试 + 细节调整 | 全部 | 1.5天 |
| **合计** | | **~14.5天** |

### 优先级

**P0 — 用户感知最明显（~5天）**
- 系列颜色（Line/Bar/Pie/Scatter）
- Pie Chart 全面补全
- Gauge min/max 接入

**P1 — 重要功能（~5天）**
- Table 高级配置
- Stat 补全
- Line/Bar 补全（数据点、connect null、value label）

**P2 — 锦上添花（~4.5天）**
- Map 补全
- Value Mappings 通用化
- Tooltip 配置

---

## 第二部分：新 Chart Type 开发

> Box Plot 不是 Grafana 原生内置类型（仅插件支持），不列入计划。
> Flame Graph、Node Graph、Logs、Traces 与工业数据场景无关，不列入计划。

---

### 1. Histogram（直方图）

**适用场景：** 传感器数据分布分析、质量控制、异常值检测

#### Config UI（对齐 Grafana）

**Histogram 选项**
| 配置项 | 说明 | 可选值 |
|--------|------|--------|
| Bucket Size | 桶宽度 | auto / 手动数值 |
| Bucket Count | 桶数量（auto 时生效） | 数值，默认 30 |
| Bucket Offset | 分桶起始偏移量 | 0~1 |
| Combine Series | 将所有系列合并为一个直方图 | 开/关 |
| Negative Values | 负值处理方式 | ignore / clip |

**Bar 样式**
| 配置项 | 说明 | 可选值 |
|--------|------|--------|
| Fill Opacity | 填充透明度 | 0~100 |
| Line Width | 柱边框线宽 | 0~10 |
| Gradient Mode | 渐变模式 | none / opacity / hue / scheme |

**Tooltip**
| 配置项 | 说明 | 可选值 |
|--------|------|--------|
| Tooltip Mode | 悬停显示模式 | single / all / hidden |
| Sort Order | 多系列排序 | none / ascending / descending |

**Axis**
| 配置项 | 说明 | 可选值 |
|--------|------|--------|
| X Axis Label | X轴标签 | 文本 |
| X Axis Min / Max | X轴范围 | 数值 |
| Y Axis Label | Y轴标签 | 文本 |
| Y Axis Scale | Y轴刻度类型 | linear / log(2) / log(10) / sqrt |
| Y Axis Soft Min / Max | Y轴软限制 | 数值 |
| Y Axis Placement | Y轴位置 | left / right / hidden |

#### 开发任务

| 任务 | 说明 |
|------|------|
| 数据处理 | 客户端分桶计算，或利用 TDengine histogram 函数 |
| ECharts 渲染 | bar 类型模拟直方图，X轴为数值范围区间 |
| Config UI | 上述所有配置项 |
| Panel 框架集成 | PanelType 注册、查询格式适配 |

**工作量：3天**

---

### 2. Heatmap（热力图）

**适用场景：** 时间模式分析（哪个时段故障多）、多设备状态对比、工艺参数热力分布

#### Config UI（对齐 Grafana）

**Heatmap 选项**
| 配置项 | 说明 | 可选值 |
|--------|------|--------|
| Calculate from Data | 是否由 panel 自动聚合为热力图 | 开/关 |
| X Bucket Size | X轴分桶时间间隔（自动聚合时） | 时间间隔，如 1h |
| Y Bucket Size | Y轴分桶大小 | 数值 |
| Y Bucket Scale | Y轴分桶刻度类型 | linear / log(2) / log(10) / symlog |

**颜色**
| 配置项 | 说明 | 可选值 |
|--------|------|--------|
| Color Scheme | 颜色方案 | Spectral / RdYlGn / Blues 等多种 |
| Min（Start） | 颜色映射最小值 | 数值（默认系列最小值） |
| Max（End） | 颜色映射最大值 | 数值（默认系列最大值） |
| Steps | 颜色分级数量 | 1~128 |
| Reverse | 反转颜色方案 | 开/关 |

**单元格显示**
| 配置项 | 说明 | 可选值 |
|--------|------|--------|
| Hide Zero | 不渲染值为 0 的单元格 | 开/关 |
| Cell Gap | 单元格间距 | 0~25 px |
| Cell Radius | 单元格圆角 | 0~50% |
| Show Values | 单元格内显示数值 | auto / never / always |

**Y 轴**
| 配置项 | 说明 | 可选值 |
|--------|------|--------|
| Placement | Y轴位置 | left / right / hidden |
| Reverse | 反转Y轴 | 开/关 |
| Min / Max | Y轴范围 | 数值 |
| Axis Width | 轴宽度 | 数值 |
| Label | 轴标签 | 文本 |

**X 轴**
| 配置项 | 说明 | 可选值 |
|--------|------|--------|
| Show | 显示/隐藏X轴 | 开/关 |
| Time Format | 时间显示格式 | 文本 |

**Tooltip**
| 配置项 | 说明 | 可选值 |
|--------|------|--------|
| Show Tooltip | 显示悬停提示 | 开/关 |
| Show Histogram | Tooltip 中显示 Y 轴分布直方图 | 开/关 |

#### 开发任务

| 任务 | 说明 |
|------|------|
| 数据处理 | 将时序数据聚合为二维网格（时间 × 指标/设备） |
| ECharts 渲染 | heatmap 类型 + visualMap 颜色映射 |
| Config UI | 上述所有配置项 |
| Panel 框架集成 | 查询格式适配 |

**工作量：4天**

---

### 3. Candlestick（K线图）

**适用场景：** 展示时间窗口内 min/max/first/last，工艺参数周期汇总，生产批次对比

#### Config UI（对齐 Grafana）

**Candlestick 选项**
| 配置项 | 说明 | 可选值 |
|--------|------|--------|
| Visualization Mode | 显示模式 | candles / volume / both |
| Candle Style | K线样式 | candles（填充）/ OHLC bars |
| Color Strategy | 颜色判断策略 | Since Open（当前周期内涨跌）/ Since Prior Close（跨周期涨跌） |
| Up Color | 上涨颜色 | 颜色选择器 |
| Down Color | 下跌颜色 | 颜色选择器 |

**字段映射**
| 配置项 | 说明 |
|--------|------|
| Open | 映射到开盘值的字段（工业场景：周期首值） |
| High | 映射到最高值的字段 |
| Low | 映射到最低值的字段 |
| Close | 映射到收盘值的字段（工业场景：周期末值） |
| Volume | 映射到成交量的字段（可选） |

**附加维度**
| 配置项 | 说明 | 可选值 |
|--------|------|--------|
| Include | 额外显示的字段（如均线） | 多选字段 |
| Ignore | 排除不显示的字段 | 多选字段 |

**堆叠**
| 配置项 | 说明 | 可选值 |
|--------|------|--------|
| Stack | 堆叠模式 | off / normal / 100% |

**Tooltip**
| 配置项 | 说明 | 可选值 |
|--------|------|--------|
| Tooltip Mode | 悬停显示模式 | single / all / hidden |

**Axis**
| 配置项 | 说明 | 可选值 |
|--------|------|--------|
| Y Axis Min / Max | Y轴范围 | 数值 |
| Y Axis Label | Y轴标签 | 文本 |
| Y Axis Placement | Y轴位置 | left / right / hidden |
| Y Axis Width | 轴宽度 | 数值 |

#### 开发任务

| 任务 | 说明 |
|------|------|
| SQL 层 | 查询返回 open/high/low/close 四个值（时间窗口首/最大/最小/末值） |
| ECharts 渲染 | candlestick 类型，支持 volume overlay |
| Config UI | 上述所有配置项 |
| Panel 框架集成 | 特殊查询格式注册 |

**工作量：3天**

---

### 4. Sankey / Flow Chart（流向图）

**适用场景：** 能耗流向、物料流转、工艺流程可视化

> 注：Grafana 无原生 Sankey，配置项参考 ECharts Sankey 能力设计。

#### Config UI

| 配置项 | 说明 | 可选值 |
|--------|------|--------|
| Direction | 流向方向 | LR（左→右）/ TB（上→下） |
| Node Alignment | 节点对齐方式 | left / right / center / justify |
| Node Width | 节点矩形宽度 | 数值 px |
| Node Gap | 节点间距 | 数值 px |
| Node Colors | 节点颜色 | 每个节点独立配色 |
| Edge Opacity | 连线透明度 | 0~1 |
| Show Labels | 显示节点标签 | 开/关 |
| Label Position | 标签位置 | inside / outside |
| Tooltip | 悬停显示流量值 | 开/关 |

#### 开发任务

| 任务 | 说明 |
|------|------|
| 数据模型 | 节点 + 边的数据结构，需特殊查询或手动配置 |
| ECharts 渲染 | sankey 类型 |
| Config UI | 上述所有配置项 |
| Panel 框架集成 | 数据格式与时序差异大，需单独适配 |

**工作量：3天**

---

### 工作量汇总

| Chart Type | 工业场景价值 | 工作量 |
|-----------|:-----------:|:------:|
| Histogram | ⭐⭐⭐⭐⭐ | 3天 |
| Heatmap | ⭐⭐⭐⭐⭐ | 4天 |
| Candlestick | ⭐⭐⭐⭐ | 3天 |
| Sankey / Flow | ⭐⭐⭐ | 3天 |
| **合计** | | **~13天** |

### 优先级

**P0 — 工业场景最高频（~7天）**
- **Histogram** — 质量控制、分布分析，几乎每个工厂都需要
- **Heatmap** — 时间模式直觉可视化，Grafana 用户高频使用

**P1 — 有差异化价值（~3天）**
- **Candlestick** — 时间窗口汇总，直观展示数据波动范围，与 TDengine 窗口函数天然契合

**P2 — 按需开发（~3天）**
- **Sankey** — 场景特定，数据准备复杂，有明确需求再开发

---

## 第三部分：AI 辅助编程模式

### 每个 Chart Type 的标准工作流

```
1. 读代码（10分钟）
   └── 让 AI 读现有 *Properties.vue + 渲染代码
       了解当前数据结构和 ECharts option 生成方式

2. 写规格（5分钟）
   └── 明确告诉 AI：加哪些字段、可选值是什么
       直接用本文档的 Config UI 表格作为 prompt 输入

3. AI 生成（5~15分钟）
   └── 同时生成三个地方：
       ① TypeScript interface 新增字段
       ② *Properties.vue 新增表单控件
       ③ 渲染代码中 ECharts option 的映射

4. 人工审查（10~20分钟）
   └── 检查逻辑正确性、边界值、默认值

5. 浏览器验证（15~30分钟）
   └── 手动测试每个配置项是否生效

6. 修复迭代（0~30分钟）
   └── 视情况而定，ECharts option 映射错误最常见
```

### 关键原则

**先做一个模板，再批量复制**

不要每个 chart type 都从零开始。先把一个最复杂的做完（建议先做 Line Chart 系列颜色），形成可复用的模式：颜色选择器组件怎么写、ECharts series 的 color 字段怎么映射，之后其他 chart type 直接套用，速度提升 30~40%。

**用本文档的表格直接作为 prompt**

```
请帮我为 Pie Chart 补充以下配置项：
- Donut 模式：inner radius 0~100，默认 0
- Slice 颜色：每个 slice 独立颜色选择器
- 标签显示：name/value/percent/组合，下拉选择
相关源代码在：
- ~/TDasset/frontend/src/views/1-explorer/views/panel/pieProperties.vue
- ~/TDasset/frontend/src/utils/panelQuery.ts
```

使用 Claude Code 等 AI 编程工具时，直接告知源文件路径即可，AI 会自行读取，无需手动粘贴代码。

**新 Chart Type 的特殊步骤**

```
1. 先让 AI 写一个最简 ECharts demo（无配置项）
2. 确认渲染正确后，再逐步加 Config UI
3. 数据查询适配最后做，最容易出问题
```

### AI 参与度分析

| 工作类型 | AI 参与度 | 说明 |
|---------|:--------:|------|
| TypeScript interface 修改 | 极高 | 接近 0 成本，AI 瞬间完成 |
| 重复性表单控件 | 极高 | slider/radio/color picker 一次生成整个 section |
| ECharts option 映射 | 高 | AI 对 ECharts API 非常熟悉，基本一次到位 |
| 单元测试（option 生成函数） | 高 | AI 可直接生成 |
| 测试用例清单 | 高 | AI 生成清单，人工执行 |
| E2E 测试脚本 | 中 | AI 可写 Playwright/Cypress，但维护成本较高 |
| 视觉正确性验证 | 低 | 需人眼判断图表渲染是否正确，难以自动化 |
| 多图层架构设计（Map） | 低 | 架构决策需人工把关 |

---

## 总体工作量

| 类别 | 工作量 |
|------|:------:|
| 第一部分：现有 Chart Type 配置补全 | ~14.5天 |
| 第二部分：新 Chart Type 开发 | ~13天 |
| **总计** | **~27.5天** |
