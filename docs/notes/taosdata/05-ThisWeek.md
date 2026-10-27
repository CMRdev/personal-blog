- 重构合并分组逻辑：（给我中文plan,不需要加载项目中的skill）

- 新建GridManager.js的Class类，用来统一管理panel、group数据，封装panel/group坐标及大小变换方法，通过创建GridManager实例的方法来管理各种操作。
  - 1 多选panel或group后，计算出整体layout位置：leftTop、rightTop、rightBottom、leftBottom，创建分组newGroup，newGroup的位置及大小为：{x: left, y: top, w: right - left, h: bottom - top }
    - 1.1 若多选的都是panel不包含group，则newGroup的h = bottom - top + 1
  - 2 需要构建两个转换函数（注：1、root和group都依据48列来计算；2、root和group使用的是相同的cellHeight，所以高度height不需要转换；3、group内部panel的row、column、width都是相对于所在group的）
    - 2.1 panel从root进入group，group要有监听，当panel，hover进来的时候，panel的row、column、width都要重新赋值，保持panel的吸附背景要和之前视觉上一样大
    - 2.2 panel从group进入root，root要有监听，当panel，hover进来的时候，panel的row、column、width都要重新赋值，保持panel的吸附背景要和之前视觉上一样大
    - 2.3 hover的时候做了坐标变换了已经那么drop的时候就不需要了。
  - 3 多选的都是panel的时候，若在这个范围内有其他otherPanel或otherGroup，则在newGroup创建完成后，将otherPanel和otherGroup依次移动到dashboard的末尾，成为末尾元素
    - 3.1 关于如何判断otherPanel或otherGroup是否在newGroup范围内，可以提取一个性能高的判断方法（可以根据rect的四点是否和newGroup的rect四点是否有交叉来判断）
  - 4 多选有group的时候，则将第一个 group1 的位置及大小设置为步骤1计算出的结果，panel都进入这个 group1，其他group自动删除
  - 5 验证：合并到一个分组后，视觉上panel相对于root的位置不变的，panel的大小不变


- 【X】当groupA高度比较小，把panel移入groupA的时候，目前的效果是drop后，自动扩大groupA。需要改一下扩大groupA的时刻，改成acceptWeigets的时候就自动扩大groupA
- 优化效果：拖拽面板panel添加到一个装不下内容的groupA的时候，检测groupA下方是否有panel或group，如果有的话就不需要自动增高groupA


- 只有面板模版、仪表板模版会存储namePattern字段。使用panel/dashboard模版生成的panel/dashboard则需要在初始生成的时候使用namePattern来生成name，然后删除namePattern属性
- 当使用namePattern来显示名称时，元素名称、模版名称无论是具体的值，还是i18n的占位符描述，都需要加上token背景
- 封装一个通用的替换字符串方法到namePatternUtils中，所有地方统一使用这个方法来替换字符串
- 所有列表页、面包屑不需要替换字符串，直接用name字段显示，这样更简单。需要处理替换字符串的地方是echart标题、面板卡片标题
- 使用supperpower来完善我的plan
