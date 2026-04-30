# 周记

## 工作计划排期

> ### 📅 总排期：2026/4/2（周四）→ 2026/6/3（周二），共 42 个工作日
>
> 排期规则：每项纯开发工时 × 1.3（含 20% 测试 + 10% 其他Bug 修复），向上取整至整天。周末休息，五一（5/1~5/5）放假。
> 策略：先完成所有现有 Chart Type 配置补全，再统一开发新 Chart Type。

### 周视图

| 周次 |    日期     | 任务 & 人天                                                         | 周工作量 |
| :--: | :---------: | ------------------------------------------------------------------- | :------: |
|  W1  |  4/2 ~ 4/3  | 系列颜色 **2天**                                                    |   2天    |
|  W2  | 4/6 ~ 4/10  | Pie **2天** · Gauge **1天** · Bar Gauge 多指标 **2天**              |   5天    |
|  W3  | 4/13 ~ 4/17 | Bar Gauge 多指标 **1天** · Table **3天** · Stat **1天**             |   5天    |
|  W4  | 4/20 ~ 4/24 | Line/Bar **2天** · Map **3天**                                      |   5天    |
|  W5  | 4/27 ~ 4/30 | Map **4天**                                                         |   4天    |
|  —   |  5/1 ~ 5/5  | 🎉 **五一假期**                                                     |    —     |
|  W6  |  5/6 ~ 5/8  | Text **1天** · V-Mappings **1天** · Tooltip **1天** ✅ 配置补全交付 |   3天    |
|  W7  | 5/9 ~ 5/15  | Histogram **4天** · Heatmap **1天**                                 |   5天    |
|  W8  | 5/18 ~ 5/22 | Heatmap **5天**                                                     |   5天    |
|  W9  | 5/25 ~ 5/29 | Candlestick **4天** · Sankey **1天**                                |   5天    |
| W10  |  6/1 ~ 6/3  | Sankey **3天** ✅ 全部交付                                          |   3天    |

## grafana 调研

|  `CHART-TYPE/OPTIONS`  | Trend Chart  | Bar Chart | Pie Chart | Gauge Chart |      Table      | Scatter Chart | Rich Text | Stat Value  |       Map        | State TimeLine | Status History | Bar Gauge |
| :--------------------: | :----------: | :-------: | :-------: | :---------: | :-------------: | :-----------: | :-------: | :---------: | :--------------: | :------------: | :------------: | :-------: |
|     Panel options      |      ✅      |    ✅     |    ✅     |     ✅      |       ✅        |      ✅       |    ✅     |     ✅      |        ✅        |       ✅       |       ✅       |    ✅     |
|                        |              | Bar chart | Pie chart |    Gauge    |      Table      |               |   Text    | Stat styles |                  | State timeline | Status history | Bar gauge |
|        Tooltip         |      ✅      |    ✅     |    ✅     |             |                 |      ✅       |           |             |                  |       ✅       |       ✅       |           |
|         Legend         |      ✅      |    ✅     |    ✅     |             |                 |      ✅       |           |             |                  |       ✅       |                |    ❌     |
|       Text size        |              |    ❌     |           |     ✅      |                 |               |           |     ✅      |                  |                |                |    ✅     |
|          Axis          |      ✅      |    ✅     |           |             |                 |      ✅       |           |             |                  |       ✅       |       ✅       |           |
|                        | Graph styles |           |           |             |                 |               |           |             |                  |                |                |           |
|                        |              |           |           |             | Table footer 🎈 |               |           |             |   Map View 🎈    |                |                |           |
|                        |              |           |           |             | Cell options 🎈 |               |           |             |  Map Layers 🎈   |                |                |           |
|                        |              |           |           |             |                 |               |           |             | Basemap layer 🎈 |                |                |           |
|                        |              |           |           |             |                 |               |           |             | Map controls 🎈  |                |                |           |
|    Standard options    |      ✅      |    ✅     |    ✅     |     ✅      |       ❌        |      ✅       |           |     ✅      |                  |       ✅       |       ✅       |    ✅     |
| Data links and actions |      ✅      |    ✅     |    ✅     |     ✅      |       ❌        |      ✅       |           |     ✅      |                  |       ✅       |       ✅       |    ✅     |
|     Value Mappings     |      ✅      |    ✅     |    ✅     |     ✅      |       ❌        |      ✅       |           |     ✅      |                  |       ✅       |       ✅       |    ✅     |
|       Thresholds       |      ✅      |    ✅     |           |     ✅      |       ❌        |      ✅       |           |     ✅      |                  |       ✅       |       ✅       |    ✅     |

### 0. Configuration Options Required

- Panel Options

  |        options         | status | suggestion                                               | Feasible | Implement Date |
  | :--------------------: | :----: | :------------------------------------------------------- | :------: | :------------: |
  |          Name          |   ✅   |                                                          |          |                |
  |      Description       |   ✅   |                                                          |          |                |
  |  Categories(TDasset)   |   ✅   |                                                          |          |                |
  | Transparent background |   ✅   | 我们的echart图没有前景色，默认都是Transparent background |    ✅    |                |

- Standard Options [ ✅ ]
  - `可以单独封装出组件，适配所有类型chart`

  |   options    | status | suggestion                                           | Feasible | Implement Date |
  | :----------: | :----: | :--------------------------------------------------- | :------: | :------------: |
  |     Unit     |        | 我们的unit是和数据绑定的，不支持unit切换             |    ❌    |                |
  |     Min      |        | 会影响Gauge类型chart                                 |    ✅    |                |
  |     Max      |        |                                                      |    ✅    |                |
  |   Decimals   |        |                                                      |    ✅    |                |
  | Display name |        | Legend的名字                                         |    ❌    |                |
  | Color Schema |        | 可封装组件在系统中内置多种配色，会中度影响现在的代码 |    ✅    |                |
  |   No Value   |        | 没有值时显示的内容                                   |    ✅    |                |

- Data Links [ ✅ ]

  |   Option   | Status | Suggestion | Feasible | Implement Date |
  | :--------: | :----: | :--------: | :------: | :------------: |
  | Data Links |   ✅   |  后期添加  |    ✅    |                |
  |  Actions   |   ❌   |            |    ❌    |                |

- Value Mappings
  - `可封装成单独组件，适配所有类型chart`

    |       Option       | Status | Suggestion | Feasible | Implement Date |
    | :----------------: | :----: | :--------: | :------: | :------------: |
    | Add value Mappings |   ✅   |  中度影响  |    ✅    |                |

- Thresholds
  - `可封装成单独组件，适配所有类型chart`

    |     Option      | Status | Suggestion | Feasible | Implement Date |
    | :-------------: | :----: | :--------: | :------: | :------------: |
    |  Add Threshold  |   ✅   |  中度影响  |    ✅    |                |
    | Thresholds mode |   ✅   |  中度影响  |    ✅    |                |
    | Show Thresholds |   ❌   |  中度影响  |    ✅    |                |

### 1. Trend Chart

- Tooltip
  - `可封装成单独组件，适配必要的类型chart`

  |     Option      | Status |     Suggestion      | Feasible | Implement Date |
  | :-------------: | :----: | :-----------------: | :------: | :------------: |
  |  Tooltip mode   |   ✅   | single、all、hidden |    ✅    |                |
  | Hover proximity |   ❌   |                     |    ✅    |                |
  |    Max width    |   ✅   |                     |    ✅    |                |

- Legend
  - `可封装成单独组件，适配所有类型chart`

  |  options   | status | Suggestion | Feasible | Implement Date |
  | :--------: | :----: | :--------- | :------: | :------------: |
  | Visibility |   ✅   |            |          |                |
  |    Mode    |   ✅   |            |          |                |
  | Placement  |   ✅   |            |          |                |
  |   Values   |   ✅   |            |          |                |

- Text Size
  - `可封装成单独组件，适配需要的类型chart`

  | Option | Status | Suggestion | Feasible | Implement Date |
  | :----: | :----: | :--------: | :------: | :------------: |
  | Title  |   ✅   |            |          |                |
  | Value  |   ✅   |            |          |                |

- Axis

  |     options     | status | Suggestion                  | Feasible | Implement Date |
  | :-------------: | :----: | :-------------------------- | :------: | :------------: |
  |    Placement    |   ✅   |                             |          |                |
  |      Label      |   ✅   |                             |          |                |
  |      Width      |   ❌   | tick宽度                    |    ✅    |                |
  | Show grid lines |   ❌   | 背景网格                    |    ✅    |                |
  |      Color      |   ❌   | tick颜色                    |    ✅    |                |
  |      Scale      |   ❌   | Linear、Logarithmic、Symlog |    ❌    |                |
  |  Centered zero  |   ❌   |                             |    ❌    |                |

- Graph Style

  |       options       | status | Suggestion               | Feasible | Implement Date |
  | :-----------------: | :----: | :----------------------- | :------: | :------------: |
  |        Style        |   ✅   |                          |          |                |
  | Line interpolation  |   ✅   |                          |          |                |
  |     Line width      |   ✅   |                          |          |                |
  |    Fill opacity     |   ✅   |                          |          |                |
  |    Gradient mode    |   ❌   | 渐变模式                 |    ❌    |                |
  |     Line style      |   ✅   |                          |          |                |
  | Connect null values |   ❌   | Never、Always、Threshold |    ✅    |                |
  |     Show Points     |   ❌   |                          |    ✅    |                |
  |     Point size      |   ❌   |                          |    ✅    |                |
  |    Stack series     |   ✅   |                          |          |                |

### 2. Bar Chart

- Bar Chart

  |            Option             | Status |    Suggestion     | Feasible | Implement Date |
  | :---------------------------: | :----: | :---------------: | :------: | :------------: |
  |             xAxis             |   ❌   | x轴显示的系列名称 |    ❌    |                |
  |          Orientation          |   ✅   |                   |          |                |
  |   Rotate X-axis tick labels   |   ✅   |                   |          |                |
  | X-axis labels minimum spacing |   ✅   |                   |          |                |
  |          Show values          |   ✅   |                   |    ✅    |                |
  |           Stacking            |   ✅   |                   |          |                |
  |          Group width          |   ❌   |                   |    ✅    |                |
  |           Bar width           |   ✅   |                   |          |                |
  |          Bar radius           |   ✅   |                   |    ✅    |                |
  | Highlight full area on hover  |   ❌   |                   |    ✅    |                |
  |        Color by field         |   ❌   |                   |    ❌    |                |
  |          Line width           |   ✅   |                   |    ✅    |                |
  |         Full Opacity          |   ✅   |                   |    ✅    |                |
  |         Gradient mode         |   ✅   |                   |    ✅    |                |

### 3. Pie Chart

- Pie chart

  |     Option     | Status | Suggestion | Feasible | Implement Date |
  | :------------: | :----: | :--------: | :------: | :------------: |
  | Pie chart type |   ❌   | Pie、Donut |    ✅    |                |
  | Slice sorting  |   ❌   |            |    ✅    |                |
  |     Labels     |   ❌   |            |    ✅    |                |

### 4. Gauge Chart

- Gauge

  |      Option      | Status |         Suggestion          | Feasible | Implement Date |
  | :--------------: | :----: | :-------------------------: | :------: | :------------: |
  |      Style       |   ✅   |         Circle、Arc         |    ✅    |                |
  |   Orientation    |   ✅   |                             |          |                |
  |    Gauge size    |   ✅   |                             |    ✅    |                |
  | Bar width factor |   ✅   |                             |    ✅    |                |
  |     Segments     |   ✅   |                             |    ✅    |                |
  | Segment spacing  |   ✅   |                             |    ✅    |                |
  |    Text mode     |   ✅   |                             |    ✅    |                |
  |  Neutral value   |   ❌   |                             |    ✅    |                |
  |  Show sparkline  |   ✅   |                             |          |                |
  | Show thresholds  |   ✅   |                             |    ✅    |                |
  |   Show labels    |   ✅   |                             |    ✅    |                |
  |      Effect      |   ✅   | Gradient BarGlow CenterGlow |    ✅    |                |

- 支持多个属性显示在一个 gauge 里面，可以选择隐藏一个或者多个属性。 [ ✅ 查询出多少显示多少 ]

- 选择一个属性以后，需要配置下面的图形属性

  |     options      | status | Suggestion | Feasible | Implement Date |
  | :--------------: | :----: | :--------: | :------: | :------------: |
  |    主题的大小    |   ❌   |            |          |                |
  |    主题的颜色    |   ❌   |            |          |                |
  | 是否需要显示指针 |   ✅   |            |          |                |

### 5. Table

- Table

  |        Option        | Status | Suggestion | Feasible | Implement Date |
  | :------------------: | :----: | :--------: | :------: | :------------: |
  |  Show table header   |   ❌   |            |    ✅    |                |
  |    Frozen columns    |   ❌   |            |    ✅    |                |
  |     Cell height      |   ❌   |            |    ✅    |                |
  |    Max row height    |   ❌   |            |    ✅    |                |
  |  Enable pagination   |   ❌   |            |    ✅    |                |
  | Minimun column width |   ❌   |            |    ✅    |                |
  |     Column width     |   ❌   |            |    ✅    |                |
  |   Column alignment   |   ❌   |            |    ✅    |                |
  |      wrap text       |   ❌   |            |    ✅    |                |
  |   wrap header text   |   ❌   |            |    ✅    |                |
  |    Column filter     |   ❌   |            |    ✅    |                |

- Table footer

  |   Option    | Status | Suggestion | Feasible | Implement Date |
  | :---------: | :----: | :--------: | :------: | :------------: |
  | Calculation |   ❌   |            |    ✅    |                |

- Cell options

  |         Option          | Status | Suggestion | Feasible | Implement Date |
  | :---------------------: | :----: | :--------: | :------: | :------------: |
  |        Cell type        |   ❌   |            |    ✅    |                |
  | Background display mode |   ❌   |            |    ✅    |                |
  |   Apply to entire row   |   ❌   |            |    ✅    |                |
  |   Cell value inspect    |   ❌   |            |    ✅    |                |
  |   Tooltip from field    |   ❌   |            |    ✅    |                |
  |   Styling from field    |   ❌   |            |    ✅    |                |

### 6. Scatter Chart

### 7. Rich Text

- Text

  | Option | Status |      Suggestion      | Feasible | Implement Date |
  | :----: | :----: | :------------------: | :------: | :------------: |
  |  Mode  |   ❌   | Markdown、Html、Code |    ❌    |                |

### 8. Stat

- Stat Style

  |       Option        | Status |    Suggestion    | Feasible | Implement Date |
  | :-----------------: | :----: | :--------------: | :------: | :------------: |
  |     Orientation     |   ✅   |                  |          |                |
  |      Text mode      |   ✅   |                  |    ✅    |                |
  |     Color mode      |   ✅   |                  |    ✅    |                |
  |     Graph mode      |   ✅   |    None、Area    |    ✅    |                |
  |   Text alignment    |   ✅   |                  |    ✅    |                |
  | Show percent change |   ❌   | 需缓存上一次数据 |    ❌    |                |

### 9. Map

- `暂时不做，目前只支持上传geoJson文件`

### 11. State Timeline

- State timeline

  |             Option             | Status | Suggestion | Feasible | Implement Date |
  | :----------------------------: | :----: | :--------: | :------: | :------------: |
  | Merge equal consecutive values |   ❌   |            |    ✅    |                |
  |          Show values           |   ❌   |            |    ✅    |                |
  |          Align values          |   ❌   |            |    ✅    |                |
  |           Row height           |   ✅   |            |          |                |
  |           Page size            |   ❌   |            |    ❌    |                |
  |           Line width           |   ✅   |            |          |                |
  |          Fill opacity          |   ✅   |            |          |                |
  |      Connect null values       |   ❌   |            |    ✅    |                |
  |       Disconnect values        |   ❌   |            |    ✅    |                |

### 10. Status History

- Status history

  |    Option    | Status | Suggestion | Feasible | Implement Date |
  | :----------: | :----: | :--------: | :------: | :------------: |
  | Show values  |   ❌   |            |    ✅    |                |
  |  Row height  |   ✅   |            |          |                |
  | Column width |   ✅   |            |          |                |
  |  Page size   |   ❌   |            |    ❌    |                |
  |  Line width  |   ✅   |            |          |                |
  | Fill opacity |   ✅   |            |          |                |

### 11. Bar Gauge

- Bar Gauge

  |       Option       | Status |    Suggestion    | Feasible | Implement Date |
  | :----------------: | :----: | :--------------: | :------: | :------------: |
  |    Orientation     |   ✅   |                  |          |                |
  |    Display mode    |   ✅   |                  |          |                |
  |   Value Display    |   ✅   |                  |          |                |
  | Show unfilled area |   ❌   | 显示灰色柱条背景 |    ✅    |                |
