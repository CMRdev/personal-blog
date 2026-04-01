# IDMP Chart 可视化能力提升计划

> 基于现有代码分析，对比 Grafana 配置能力制定。以下功能已由其他方式处理，不列入本计划：
> 单位系统、小数位数（已有其他处理方式）、Reduce 函数（SQL层处理）、Overrides 系统（不需要）、Legend / Data Links / Standard Options（通用组件已实现，所有 chart type 均已支持）。
>
> 工作量估算基于 AI 辅助编程（Claude Code），具体工作模式见第三部分。

---

## 第一部分：现有 Chart Type 配置补全

### 1. Line Chart (Trend)

| 配置项                          | 现状 | 待补充说明                 |
| ------------------------------- | :--: | -------------------------- |
| Title / SubTitle                |  ✅  |                            |
| Line Style (lines/step/smooth)  |  ✅  |                            |
| Step Interpolation              |  ✅  |                            |
| Line Type (solid/dashed/dotted) |  ✅  |                            |
| Line Width                      |  ✅  |                            |
| Line Opacity                    |  ✅  |                            |
| Fill Opacity                    |  ✅  |                            |
| Label Rotate / Interval         |  ✅  |                            |
| Stack Mode                      |  ✅  |                            |
| Multi-lane                      |  ✅  |                            |
| Y轴（左/右，title/min/max）     |  ✅  |                            |
| Limits / Thresholds             |  ✅  |                            |
| 系列颜色                        |  ❌  | 每条线独立配色             |
| 显示数据点                      |  ❌  | auto/never/always + 点大小 |
| Gradient Fill Mode              |  ❌  | none/opacity/hue/scheme    |
| Connect Null Values             |  ❌  | none/linear/threshold      |
| Tooltip 模式                    |  ❌  | single/all/hidden          |
| X轴配置                         |  ❌  | 显示/隐藏、时间格式        |
| Legend                          |  ❌  |                            |
| Standard Options                |  ⚠️  | 需要调试                   |
| Data Links                      |  ⚠️  | 需要调试                   |
| Value Mappings                  |  ⚠️  | 需要调试                   |
| Thresholds                      |  ⚠️  | 需要调试                   |

---

### 2. Bar Chart

| 配置项                  | 现状 | 待补充说明               |
| ----------------------- | :--: | ------------------------ |
| Title / SubTitle        |  ✅  |                          |
| Orientation             |  ✅  |                          |
| Bar Width / Opacity     |  ✅  |                          |
| Label Rotate / Interval |  ✅  |                          |
| Stack Mode              |  ✅  |                          |
| Y轴                     |  ✅  |                          |
| Limits                  |  ✅  |                          |
| 系列颜色                |  ❌  | 每根柱独立配色           |
| 柱上 Value Label        |  ❌  | 显示/隐藏、位置、字号    |
| Tooltip 模式            |  ❌  | single/all/hidden        |
| X轴配置                 |  ❌  | 显示/隐藏、时间格式      |
| Text size               |  ❌  | 设置title、value字体大小 |
| Standard Options        |  ⚠️  | 需要调试                 |
| Data Links              |  ⚠️  | 需要调试                 |
| Value Mappings          |  ⚠️  | 需要调试                 |
| Thresholds              |  ⚠️  | 需要调试                 |

---

### 3. Pie Chart

| 配置项           | 现状 | 待补充说明              |
| ---------------- | :--: | ----------------------- |
| Title            |  ✅  |                         |
| Donut 模式       |  ❌  | 内圆半径可调            |
| Slice 颜色       |  ❌  | 每个 slice 独立颜色     |
| 标签显示         |  ❌  | name/value/percent/组合 |
| 标签位置         |  ❌  | inside/outside          |
| 排序             |  ❌  | 按值升序/降序           |
| Tooltip          |  ❌  |                         |
| Stroke           |  ❌  | 边框宽度、颜色          |
| Legend           |  ❌  |                         |
| Standard Options |  ⚠️  | 需要调试                |
| Data Links       |  ⚠️  | 需要调试                |
| Value Mappings   |  ⚠️  | 需要调试                |
| Thresholds       |  ⚠️  | 需要调试                |

---

### 4. Gauge

| 配置项                  | 现状 | 待补充说明                            |
| ----------------------- | :--: | ------------------------------------- |
| Title                   |  ✅  |                                       |
| Orientation             |  ✅  |                                       |
| Display Time            |  ✅  |                                       |
| Show Threshold Labels   |  ✅  |                                       |
| Title / Value Font Size |  ✅  |                                       |
| 阈值颜色                |  ✅  | 已通过通用 Limits 组件实现            |
| Min / Max               |  ⚠️  | 模型字段已有，UI 和渲染均未接入，需补 |
| Text size               |  ❌  | 设置title、value字体大小              |
| Standard Options        |  ⚠️  | 需要调试                              |
| Data Links              |  ⚠️  | 需要调试                              |
| Value Mappings          |  ⚠️  | 需要调试                              |
| Thresholds              |  ⚠️  | 需要调试                              |

---

### 5. Stat

| 配置项                   | 现状 | 待补充说明               |
| ------------------------ | :--: | ------------------------ |
| Orientation              |  ✅  |                          |
| Display Time             |  ✅  |                          |
| Title / Value 字号、颜色 |  ✅  |                          |
| Background Color         |  ✅  |                          |
| Width                    |  ✅  |                          |
| Text 模式                |  ❌  | value/name/value+name    |
| Sparkline                |  ❌  | 背景小折线图             |
| Color 模式               |  ❌  | background/value/none    |
| Text size                |  ❌  | 设置title、value字体大小 |
| Standard Options         |  ⚠️  | 需要调试                 |
| Data Links               |  ⚠️  | 需要调试                 |
| Value Mappings           |  ⚠️  | 需要调试                 |
| Thresholds               |  ⚠️  | 需要调试                 |

---

### 6. Table

| 配置项           | 现状 | 待补充说明             |
| ---------------- | :--: | ---------------------- |
| Timestamp Format |  ✅  |                        |
| Column Aliases   |  ✅  |                        |
| 列宽             |  ❌  | auto / 固定 px         |
| 列对齐           |  ❌  | left/center/right      |
| Cell 类型        |  ❌  | 颜色背景、color-text   |
| 阈值着色         |  ❌  | 按值范围着色           |
| Footer           |  ❌  | sum/mean/min/max/count |
| 列排序           |  ❌  | 默认排序列             |
| Standard Options |  ⚠️  | 需要调试               |
| Data Links       |  ⚠️  | 需要调试               |
| Value Mappings   |  ⚠️  | 需要调试               |
| Thresholds       |  ⚠️  | 需要调试               |

---

### 7. Map（地图）

| 配置项             | 现状 | 待补充说明                                       |
| ------------------ | :--: | ------------------------------------------------ |
| GeoJSON 文件上传   |  ✅  |                                                  |
| Visual Map Min/Max |  ✅  |                                                  |
| 3色渐变            |  ✅  |                                                  |
| 显示标签           |  ✅  |                                                  |
| Basemap 类型选择   |  ❌  | OpenStreetMap / CARTO / ArcGIS / 自定义 XYZ Tile |
| 初始视图           |  ❌  | 经纬度中心点 + 缩放级别 / 自适应数据范围         |
| 地图控件           |  ❌  | 缩放按钮、鼠标滚轮缩放、比例尺、归属信息显示     |
| Markers 图层       |  ❌  | 点标记，大小/颜色/图标可按数据驱动配置           |
| Heatmap 图层       |  ❌  | 热力点叠加，radius/blur/opacity 可配置           |
| 多图层管理         |  ❌  | 添加/删除/排序多个图层                           |
| 位置模式           |  ❌  | 经纬度字段映射 / Geohash / 自动识别字段名        |
| Tooltip 模式       |  ❌  | 悬停显示 / 点击显示 / 关闭                       |
| GeoJSON 样式规则   |  ❌  | 按字段值条件着色，不只是统一渐变                 |

---

### 8. Text（富文本）

| 配置项                            | 现状 | 待补充说明                                   |
| --------------------------------- | :--: | -------------------------------------------- |
| 背景颜色                          |  ✅  |                                              |
| 背景图片                          |  ✅  |                                              |
| 背景图片布局（none/cover/repeat） |  ✅  |                                              |
| 内容渲染模式                      |  ❌  | Markdown / HTML / 纯文本，Grafana 三种都支持 |
| 变量插值                          |  ❌  | 内容中引用 dashboard 变量（Grafana 支持）    |

---

### 9. Scatter

| 配置项                                | 现状 | 待补充说明               |
| ------------------------------------- | :--: | ------------------------ |
| Title / SubTitle                      |  ✅  |                          |
| Symbol 类型 / 大小                    |  ✅  |                          |
| Opacity                               |  ✅  |                          |
| Special Points                        |  ✅  |                          |
| Label Rotate / Interval               |  ✅  |                          |
| Y轴                                   |  ✅  |                          |
| Data Analysis (clustering/regression) |  ✅  |                          |
| 系列颜色                              |  ❌  | 多系列时每个系列独立配色 |
| Tooltip                               |  ❌  |                          |
| Standard Options                      |  ⚠️  | 需要调试                 |
| Data Links                            |  ⚠️  | 需要调试                 |
| Value Mappings                        |  ⚠️  | 需要调试                 |
| Thresholds                            |  ⚠️  | 需要调试                 |

---

### 10. Bar Gauge

| 配置项                                 | 现状 | 待补充说明               |
| -------------------------------------- | :--: | ------------------------ |
| Title / SubTitle                       |  ✅  |                          |
| Orientation                            |  ✅  |                          |
| Display Time                           |  ✅  |                          |
| Display Mode (gradient/basic/retroLCD) |  ✅  |                          |
| Value Display                          |  ✅  |                          |
| Name Placement                         |  ✅  |                          |
| Bar Size (auto/manual, min/max)        |  ✅  |                          |
| Color Thresholds                       |  ✅  |                          |
| Threshold Mode (absolute/percentage)   |  ✅  |                          |
| Tooltip                                |  ❌  |                          |
| Axis                                   |  ❌  |                          |
| Text size                              |  ❌  | 设置title、value字体大小 |
| Legend                                 |  ❌  |                          |
| Standard Options                       |  ⚠️  | 需要调试                 |
| Data Links                             |  ⚠️  | 需要调试                 |
| Value Mappings                         |  ⚠️  | 需要调试                 |
| Thresholds                             |  ⚠️  | 需要调试                 |

---

### 11. State Timeline

| 配置项                  | 现状 | 待补充说明 |
| ----------------------- | :--: | ---------- |
| Title / SubTitle        |  ✅  |            |
| Border Width            |  ✅  |            |
| Row Height              |  ✅  |            |
| Fill Opacity            |  ✅  |            |
| Label Rotate / Interval |  ✅  |            |
| Limits（带颜色阈值）    |  ✅  |            |
| Tooltip                 |  ❌  |            |
| Axis                    |  ❌  |            |
| Legend                  |  ❌  |            |
| Standard Options        |  ⚠️  | 需要调试   |
| Data Links              |  ⚠️  | 需要调试   |
| Value Mappings          |  ⚠️  | 需要调试   |
| Thresholds              |  ⚠️  | 需要调试   |

---

### 12. Status History

| 配置项                    | 现状 | 待补充说明 |
| ------------------------- | :--: | ---------- |
| Title / SubTitle          |  ✅  |            |
| Value Mappings（5种类型） |  ✅  |            |
| Border Width              |  ✅  |            |
| Row Height / Column Width |  ✅  |            |
| Fill Opacity              |  ✅  |            |
| Label Rotate / Interval   |  ✅  |            |
| Tooltip                   |  ❌  |            |
| Legend                    |  ❌  |            |
| Standard Options          |  ⚠️  | 需要调试   |
| Data Links                |  ⚠️  | 需要调试   |
| Value Mappings            |  ⚠️  | 需要调试   |
| Thresholds                |  ⚠️  | 需要调试   |

---

### 13. 详细配置项

#### 0. Configuration Options Required

- Panel Options

  |        options         | status | suggestion                                               |
  | :--------------------: | :----: | :------------------------------------------------------- |
  |          Name          |   ✅   |                                                          |
  |      Description       |   ✅   |                                                          |
  |  Categories(TDasset)   |   ✅   |                                                          |
  | Transparent background |   ❌   | 我们的echart图没有前景色，默认都是Transparent background |

- Standard Options [ ❌ ]
  - `可以单独封装出组件，适配所有类型chart`

  |   options    | status | suggestion                                           |
  | :----------: | :----: | :--------------------------------------------------- |
  |     Unit     |        | 我们的unit是和数据绑定的，不支持unit切换             |
  |     Min      |        | 会影响Gauge类型chart                                 |
  |     Max      |        |                                                      |
  |   Decimals   |        |                                                      |
  | Display name |        | Legend的名字                                         |
  | Color Schema |        | 可封装组件在系统中内置多种配色，会中度影响现在的代码 |
  |   No Value   |        | 没有值时显示的内容                                   |

- Data Links [ ❌ ]

  |   Option   | Status | Suggestion |
  | :--------: | :----: | :--------: |
  | Data Links |   ❌   |  后期添加  |
  |  Actions   |   ❌   |            |

- Value Mappings
  - `可封装成单独组件，适配所有类型chart`

    |       Option       | Status | Suggestion |
    | :----------------: | :----: | :--------: |
    | Add value Mappings |   ❌   |  中度影响  |

- Thresholds
  - `可封装成单独组件，适配所有类型chart`

    |     Option      | Status | Suggestion |
    | :-------------: | :----: | :--------: |
    |  Add Threshold  |   ❌   |  中度影响  |
    | Thresholds mode |   ❌   |  中度影响  |
    | Show Thresholds |   ❌   |  中度影响  |

#### 1. Trend Chart

- Tooltip
  - `可封装成单独组件，适配必要的类型chart`

  |     Option      | Status |     Suggestion      |
  | :-------------: | :----: | :-----------------: |
  |  Tooltip mode   |   ❌   | single、all、hidden |
  | Hover proximity |   ❌   |                     |
  |    Max width    |   ❌   |                     |

- Legend
  - `可封装成单独组件，适配所有类型chart`

  |  options   | status | Suggestion |
  | :--------: | :----: | :--------- |
  | Visibility |   ✅   |            |
  |    Mode    |   ✅   |            |
  | Placement  |   ✅   |            |
  |   Values   |   ✅   |            |

- Text Size
  - `可封装成单独组件，适配需要的类型chart`

  | Option | Status | Suggestion |
  | :----: | :----: | :--------: |
  | Title  |   ❌   |            |
  | Value  |   ❌   |            |

- Axis

  |     options     | status | Suggestion                  |
  | :-------------: | :----: | :-------------------------- |
  |    Placement    |   ✅   |                             |
  |      Label      |   ✅   |                             |
  |      Width      |   ❌   | tick宽度                    |
  | Show grid lines |   ❌   | 背景网格                    |
  |      Color      |   ❌   | tick颜色                    |
  |      Scale      |   ❌   | Linear、Logarithmic、Symlog |
  |  Centered zero  |   ❌   |                             |

- Graph Style

  |       options       | status | Suggestion               |
  | :-----------------: | :----: | :----------------------- |
  |        Style        |   ✅   |                          |
  | Line interpolation  |   ✅   |                          |
  |     Line width      |   ✅   |                          |
  |    Fill opacity     |   ✅   |                          |
  |    Gradient mode    |   ❌   | 渐变模式                 |
  |     Line style      |   ✅   |                          |
  | Connect null values |   ❌   | Never、Always、Threshold |
  |     Show Points     |   ❌   |                          |
  |     Point size      |   ❌   |                          |
  |    Stack series     |   ✅   |                          |

#### 2. Bar Chart

- Bar Chart

  |            Option             | Status |    Suggestion     |
  | :---------------------------: | :----: | :---------------: |
  |             xAxis             |   ❌   | x轴显示的系列名称 |
  |          Orientation          |   ✅   |                   |
  |   Rotate X-axis tick labels   |   ✅   |                   |
  | X-axis labels minimum spacing |   ✅   |                   |
  |          Show values          |   ❌   |                   |
  |           Stacking            |   ✅   |                   |
  |          Group width          |   ❌   |                   |
  |           Bar width           |   ✅   |                   |
  |          Bar radius           |   ❌   |                   |
  | Highlight full area on hover  |   ❌   |                   |
  |        Color by field         |   ❌   |                   |
  |          Line width           |   ❌   |                   |
  |         Full Opacity          |   ❌   |                   |
  |         Gradient mode         |   ❌   |                   |

#### 3. Pie Chart

- Pie chart

  |     Option     | Status | Suggestion |
  | :------------: | :----: | :--------: |
  | Pie chart type |   ❌   | Pie、Donut |
  | Slice sorting  |   ❌   |            |
  |     Labels     |   ❌   |            |

#### 4. Gauge Chart

- Gauge

  |      Option      | Status |         Suggestion          |
  | :--------------: | :----: | :-------------------------: |
  |      Style       |   ❌   |         Circle、Arc         |
  |   Orientation    |   ✅   |                             |
  |    Gauge size    |   ❌   |                             |
  | Bar width factor |   ❌   |                             |
  |     Segments     |   ❌   |                             |
  | Segment spacing  |   ❌   |                             |
  |    Text mode     |   ❌   |                             |
  |  Neutral value   |   ❌   |                             |
  |  Show sparkline  |   ✅   |                             |
  | Show thresholds  |   ❌   |                             |
  |   Show labels    |   ❌   |                             |
  |      Effect      |   ❌   | Gradient BarGlow CenterGlow |

- 支持多个属性显示在一个 gauge 里面，可以选择隐藏一个或者多个属性。 [ ✅ 查询出多少显示多少 ]

- 选择一个属性以后，需要配置下面的图形属性

  |     options      | status | Suggestion |
  | :--------------: | :----: | :--------: |
  |    主题的大小    |   ❌   |            |
  |    主题的颜色    |   ❌   |            |
  | 是否需要显示指针 |   ✅   |            |

#### 5. Table

- Table

  |        Option        | Status | Suggestion |
  | :------------------: | :----: | :--------: |
  |  Show table header   |   ❌   |            |
  |    Frozen columns    |   ❌   |            |
  |     Cell height      |   ❌   |            |
  |    Max row height    |   ❌   |            |
  |  Enable pagination   |   ❌   |            |
  | Minimun column width |   ❌   |            |
  |     Column width     |   ❌   |            |
  |   Column alignment   |   ❌   |            |
  |      wrap text       |   ❌   |            |
  |   wrap header text   |   ❌   |            |
  |    Column filter     |   ❌   |            |

- Table footer

  |   Option    | Status | Suggestion |
  | :---------: | :----: | :--------: |
  | Calculation |   ❌   |            |

- Cell options

  |         Option          | Status | Suggestion |
  | :---------------------: | :----: | :--------: |
  |        Cell type        |   ❌   |            |
  | Background display mode |   ❌   |            |
  |   Apply to entire row   |   ❌   |            |
  |   Cell value inspect    |   ❌   |            |
  |   Tooltip from field    |   ❌   |            |
  |   Styling from field    |   ❌   |            |

#### 6. Scatter Chart

#### 7. Rich Text

- Text

  | Option | Status |      Suggestion      |
  | :----: | :----: | :------------------: |
  |  Mode  |   ❌   | Markdown、Html、Code |

#### 8. Stat

- Stat Style

  |       Option        | Status |    Suggestion    |
  | :-----------------: | :----: | :--------------: |
  |     Orientation     |   ✅   |                  |
  |      Text mode      |   ❌   |                  |
  |     Color mode      |   ❌   |                  |
  |     Graph mode      |   ❌   |    None、Area    |
  |   Text alignment    |   ❌   |                  |
  | Show percent change |   ❌   | 需缓存上一次数据 |

#### 9. State Timeline

- State timeline

  |             Option             | Status | Suggestion |
  | :----------------------------: | :----: | :--------: |
  | Merge equal consecutive values |   ❌   |            |
  |          Show values           |   ❌   |            |
  |          Align values          |   ❌   |            |
  |           Row height           |   ✅   |            |
  |           Page size            |   ❌   |            |
  |           Line width           |   ✅   |            |
  |          Fill opacity          |   ✅   |            |
  |      Connect null values       |   ❌   |            |
  |       Disconnect values        |   ❌   |            |

#### 10. Status History

- Status history

  |    Option    | Status | Suggestion |
  | :----------: | :----: | :--------: |
  | Show values  |   ❌   |            |
  |  Row height  |   ✅   |            |
  | Column width |   ✅   |            |
  |  Page size   |   ❌   |            |
  |  Line width  |   ✅   |            |
  | Fill opacity |   ✅   |            |

#### 11. Bar Gauge

- Bar Gauge

  |       Option       | Status |    Suggestion    |
  | :----------------: | :----: | :--------------: |
  |    Orientation     |   ✅   |                  |
  |    Display mode    |   ✅   |                  |
  |   Value Display    |   ✅   |                  |
  | Show unfilled area |   ❌   | 显示灰色柱条背景 |

### 工作量汇总

> 每项任务的测试工作量包含：单元测试编写、集成测试、视觉正确性验证及细节调整。测试总占比约 30%。

| 任务                                                           | 涉及 Chart                              | 开发工作量 | 测试工作量 |    合计     |
| -------------------------------------------------------------- | --------------------------------------- | :--------: | :--------: | :---------: |
| 系列颜色                                                       | Line、Bar、Scatter、Pie                 |    1天     |   0.5天    |    1.5天    |
| Pie Chart 全面补全                                             | Pie                                     |    1天     |   0.5天    |    1.5天    |
| Gauge 补全（min/max UI接入 + value mapping）                   | Gauge                                   |   0.5天    |   0.5天    |     1天     |
| Stat 补全（text模式/sparkline/color模式）                      | Stat                                    |   0.5天    |   0.5天    |     1天     |
| Table 高级配置（列宽/对齐/cell类型/footer/阈值着色）           | Table                                   |    2天     |    1天     |     3天     |
| Line/Bar 补全（数据点/connect null/value label/X轴）           | Line、Bar                               |    1天     |   0.5天    |    1.5天    |
| Map 补全（basemap/初始视图/地图控件/markers/位置模式/tooltip） | Map                                     |    5天     |    2天     |     7天     |
| Text 补全（渲染模式/变量插值）                                 | Text                                    |   0.5天    |   0.5天    |     1天     |
| Value Mappings 通用化                                          | Gauge、Bar Gauge、State Timeline、Table |   0.5天    |   0.5天    |     1天     |
| Tooltip 配置                                                   | 所有 chart                              |   0.5天    |   0.5天    |     1天     |
| **合计**                                                       |                                         | **12.5天** |  **7天**   | **~19.5天** |

### 优先级

**P0 — 用户感知最明显（~4天，含测试 ~1.5天）**

- 系列颜色（Line/Bar/Pie/Scatter）
- Pie Chart 全面补全
- Gauge min/max 接入

**P1 — 重要功能（~5.5天，含测试 ~2天）**

- Table 高级配置
- Stat 补全
- Line/Bar 补全（数据点、connect null、value label）

**P2 — 锦上添花（~10天，含测试 ~3.5天）**

- Map 补全
- Text 补全
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

| 任务           | 说明                                           |
| -------------- | ---------------------------------------------- |
| 数据处理       | 客户端分桶计算，或利用 TDengine histogram 函数 |
| ECharts 渲染   | bar 类型模拟直方图，X轴为数值范围区间          |
| Config UI      | 上述所有配置项                                 |
| Panel 框架集成 | PanelType 注册、查询格式适配                   |
| 测试验证       | 单元测试 + 分桶边界测试 + 视觉验证             |

**工作量：4.5天**（开发 3天 + 测试 1.5天）

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

| 任务           | 说明                                         |
| -------------- | -------------------------------------------- |
| 数据处理       | 将时序数据聚合为二维网格（时间 × 指标/设备） |
| ECharts 渲染   | heatmap 类型 + visualMap 颜色映射            |
| Config UI      | 上述所有配置项                               |
| Panel 框架集成 | 查询格式适配                                 |
| 测试验证       | 单元测试 + 颜色映射测试 + 视觉验证           |

**工作量：6天**（开发 4天 + 测试 2天）

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

| 任务           | 说明                                                             |
| -------------- | ---------------------------------------------------------------- |
| SQL 层         | 查询返回 open/high/low/close 四个值（时间窗口首/最大/最小/末值） |
| ECharts 渲染   | candlestick 类型，支持 volume overlay                            |
| Config UI      | 上述所有配置项                                                   |
| Panel 框架集成 | 特殊查询格式注册                                                 |
| 测试验证       | 单元测试 + OHLC 数据验证 + 视觉验证                              |

**工作量：4天**（开发 3天 + 测试 1天）

---

### 4. Sankey / Flow Chart（流向图）

**适用场景：** 能耗流向、物料流转、工艺流程可视化

> 注：Grafana 无原生 Sankey，配置项参考 ECharts Sankey 能力设计。

#### Config UI

| 配置项         | 说明           | 可选值                          |
| -------------- | -------------- | ------------------------------- |
| Direction      | 流向方向       | LR（左→右）/ TB（上→下）        |
| Node Alignment | 节点对齐方式   | left / right / center / justify |
| Node Width     | 节点矩形宽度   | 数值 px                         |
| Node Gap       | 节点间距       | 数值 px                         |
| Node Colors    | 节点颜色       | 每个节点独立配色                |
| Edge Opacity   | 连线透明度     | 0~1                             |
| Show Labels    | 显示节点标签   | 开/关                           |
| Label Position | 标签位置       | inside / outside                |
| Tooltip        | 悬停显示流量值 | 开/关                           |

#### 开发任务

| 任务           | 说明                                      |
| -------------- | ----------------------------------------- |
| 数据模型       | 节点 + 边的数据结构，需特殊查询或手动配置 |
| ECharts 渲染   | sankey 类型                               |
| Config UI      | 上述所有配置项                            |
| Panel 框架集成 | 数据格式与时序差异大，需单独适配          |
| 测试验证       | 单元测试 + 节点/边数据验证 + 视觉验证     |

**工作量：4天**（开发 3天 + 测试 1天）

---

### 工作量汇总

| Chart Type    | 工业场景价值 | 开发工作量 | 测试工作量 |    合计     |
| ------------- | :----------: | :--------: | :--------: | :---------: |
| Histogram     |  ⭐⭐⭐⭐⭐  |    3天     |   1.5天    |    4.5天    |
| Heatmap       |  ⭐⭐⭐⭐⭐  |    4天     |    2天     |     6天     |
| Candlestick   |   ⭐⭐⭐⭐   |    3天     |    1天     |     4天     |
| Sankey / Flow |    ⭐⭐⭐    |    3天     |    1天     |     4天     |
| **合计**      |              |  **13天**  | **5.5天**  | **~18.5天** |

### 优先级

**P0 — 工业场景最高频（~10.5天，含测试 ~3.5天）**

- **Histogram** — 质量控制、分布分析，几乎每个工厂都需要
- **Heatmap** — 时间模式直觉可视化，Grafana 用户高频使用

**P1 — 有差异化价值（~4天，含测试 ~1天）**

- **Candlestick** — 时间窗口汇总，直观展示数据波动范围，与 TDengine 窗口函数天然契合

**P2 — 按需开发（~4天，含测试 ~1天）**

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

| 工作类型                    | AI 参与度 | 说明                                           |
| --------------------------- | :-------: | ---------------------------------------------- |
| TypeScript interface 修改   |   极高    | 接近 0 成本，AI 瞬间完成                       |
| 重复性表单控件              |   极高    | slider/radio/color picker 一次生成整个 section |
| ECharts option 映射         |    高     | AI 对 ECharts API 非常熟悉，基本一次到位       |
| 单元测试（option 生成函数） |    高     | AI 可直接生成                                  |
| 测试用例清单                |    高     | AI 生成清单，人工执行                          |
| E2E 测试脚本                |    中     | AI 可写 Playwright/Cypress，但维护成本较高     |
| 视觉正确性验证              |    低     | 需人眼判断图表渲染是否正确，难以自动化         |
| 多图层架构设计（Map）       |    低     | 架构决策需人工把关                             |

---

## 总体工作量

| 类别                               | 开发工作量 | 测试工作量 | 合计工作量 |
| ---------------------------------- | :--------: | :--------: | :--------: |
| 第一部分：现有 Chart Type 配置补全 |   14.5天   |    8天     |  ~22.5天   |
| 第二部分：新 Chart Type 开发       |    13天    |   5.5天    |  ~18.5天   |
| **总计**                           | **27.5天** | **13.5天** | **~41天**  |

---

## 第四部分：工作计划排期

> ### 📅 总排期：2026/4/2（周四）→ 2026/6/3（周二），共 42 个工作日
>
> 排期规则：每项纯开发工时 × 1.3（含 20% 测试 + 10% 其他Bug 修复），向上取整至整天。周末休息，五一（5/1~5/5）放假。
> 策略：先完成所有现有 Chart Type 配置补全，再统一开发新 Chart Type。

### 工时明细

|  #  | 阶段 | 任务                             |   纯开发   | 排期(×1.3) |  开始 → 结束   |
| :-: | :--: | -------------------------------- | :--------: | :--------: | :------------: |
|  1  |  P0  | 系列颜色（Line/Bar/Pie/Scatter） |    1天     |  **2天**   |   4/2 → 4/3    |
|  2  |  P0  | Pie Chart 全面补全               |    1天     |  **2天**   |   4/6 → 4/7    |
|  3  |  P0  | Gauge min/max 接入               |   0.5天    |  **1天**   |   4/8 → 4/8    |
|  4  |  P0  | Bar Gauge 支持多指标             |    2天     |  **3天**   |   4/9 → 4/13   |
|  5  |  P1  | Table 高级配置                   |    2天     |  **3天**   |  4/14 → 4/16   |
|  6  |  P1  | Stat 补全                        |   0.5天    |  **1天**   |  4/17 → 4/17   |
|  7  |  P1  | Line/Bar 补全                    |    1天     |  **2天**   |  4/20 → 4/21   |
|  8  |  P2  | Map 补全                         |    5天     |  **7天**   |  4/22 → 4/30   |
|  9  |  P2  | Text 补全                        |   0.5天    |  **1天**   |   5/6 → 5/6    |
| 10  |  P2  | Value Mappings 通用化            |   0.5天    |  **1天**   |   5/7 → 5/7    |
| 11  |  P2  | Tooltip 配置                     |   0.5天    |  **1天**   |   5/8 → 5/8    |
| 12  | 新P0 | Histogram 开发                   |    3天     |  **4天**   |  5/9 → 5/14    |
| 13  | 新P0 | Heatmap 开发                     |    4天     |  **6天**   |  5/15 → 5/22   |
| 14  | 新P1 | Candlestick 开发                 |    3天     |  **4天**   |  5/23 → 5/28   |
| 15  | 新P2 | Sankey 开发                      |    3天     |  **4天**   |  5/29 → 6/3    |
|     |      | **总计**                         | **27.5天** |  **42天**  | **4/2 → 6/3**  |

### 周视图

| 周次 |    日期     | 任务 & 人天                                                                       | 周工作量 |
| :--: | :---------: | --------------------------------------------------------------------------------- | :------: |
|  W1  |  4/2 ~ 4/3  | 系列颜色 **2天**                                                                  |   2天    |
|  W2  | 4/6 ~ 4/10  | Pie **2天** · Gauge **1天** · Bar Gauge 多指标 **2天**                            |   5天    |
|  W3  | 4/13 ~ 4/17 | Bar Gauge 多指标 **1天** · Table **3天** · Stat **1天**                           |   5天    |
|  W4  | 4/20 ~ 4/24 | Line/Bar **2天** · Map **3天**                                                    |   5天    |
|  W5  | 4/27 ~ 4/30 | Map **4天**                                                                       |   4天    |
|  —   |  5/1 ~ 5/5  | 🎉 **五一假期**                                                                   |    —     |
|  W6  |  5/6 ~ 5/8  | Text **1天** · V-Mappings **1天** · Tooltip **1天** ✅ 配置补全交付               |   3天    |
|  W7  | 5/9 ~ 5/15  | Histogram **4天** · Heatmap **1天**                                               |   5天    |
|  W8  | 5/18 ~ 5/22 | Heatmap **5天**                                                                   |   5天    |
|  W9  | 5/25 ~ 5/29 | Candlestick **4天** · Sankey **1天**                                              |   5天    |
| W10  |  6/1 ~ 6/3  | Sankey **3天** ✅ 全部交付                                                        |   3天    |

---

## 总体工作量

| 类别                               | 开发工作量 | 测试工作量 | 合计工作量 |
| ---------------------------------- | :--------: | :--------: | :--------: |
| 第一部分：现有 Chart Type 配置补全 |   14.5天   |    8天     |  ~22.5天   |
| 第二部分：新 Chart Type 开发       |    13天    |   5.5天    |  ~18.5天   |
| **总计**                           | **27.5天** | **13.5天** | **~41天**  |

---

## 第五部分：风险项

| # | 风险类别 | 风险描述 | 影响程度 | 应对措施 |
|:-:|---------|---------|:-------:|---------|
| 1 | 测试覆盖 | 代码测试覆盖率目标 65%，可能因工期压缩而不达标 | 中 | 优先保障核心渲染逻辑的单元测试 |
| 2 | AI 辅助局限 | ECharts 配置项繁多易选错、自定义图元缺少参考、渲染结果需人工反复调试、数据源字段映射易猜错 | 中 | 人工查阅 ECharts 文档校正；提前准备示例代码作为 prompt 上下文；预留充足浏览器验证时间；人工审查所有数据映射逻辑 |
| 3 | 新模块工期 | Map、Histogram、Heatmap、Candlestick、Sankey 以往经验每个图表约 2 周完成 | 高 | 当前排期已按 AI 辅助提效估算，若 AI 效果不及预期需延期 |
| 4 | Map 复杂度 | Map 地图功能涉及多图层、GeoJSON、Basemap 等，工作量可能超出预期 | 高 | Map 排在 P2，可视进度决定是否裁剪功能范围 |
| 5 | 设计决策 | 部分新图表可能存在架构/交互设计问题需要讨论 | 低 | 开发前先出最简 demo 确认方案，减少返工 |
