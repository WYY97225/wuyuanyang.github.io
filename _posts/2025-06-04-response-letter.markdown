 一份值得学习的作者修改说明

from [当代经济学基金会](https://mp.weixin.qq.com/s/NDPJatFbpxGo1ohlOP-SIA)

致谢
非常感谢审稿人对论文的审读以及富有建设性的意见，审稿人意见对文章的修改与完善起到了极为重要的作用。根据审稿人的意见，我们对相关问题进行了深入思考和探讨，进行了全面地修改与完善。借此，文章质量得到了显著提升。

---

## 专家一意见回复

### 问题1：医联体数量测量的准确性
**审稿意见：**  
通过爬取县区官网信息和关键词分析识别医联体数量是否存在严重测量误差？是否所有区县都有正常运营的官网？官网是否包含医联体建设信息？识别结果占全国县区比例？与官方数据是否对应？

**作者回复：**
1. **数据收集方法优化**  
   - 采用Python爬虫技术扩大数据搜索范围（人民政府官网+卫健委官网）
   - 关键词：`医联体`和`签约`
   - 方法依据：参考医疗服务领域文献（<表1>展示相关研究）
   
2. **官网运营情况验证**  
   - 政策依据：2020年《医疗联合体管理办法》要求政府主导医联体信息公开
   - 所有区县均有人民政府官网，卫健委信息可能整合至政府官网（如北京海淀区案例<图1><图2>）
   - 医联体作为政府主导改革政策，相关信息会及时在官网发布

3. **数据校验方法**  
   - 使用国家和省级宏观数据校验爬虫数据：
     - **省级校验**：2017年国务院医改简报数据（浙江218个/陕西101个）与爬取的CFPS样本区县数据匹配（浙江3区县7个/陕西3区县3个）
     - **国家级校验**：2020年国家卫健委公布的全国医联体总数（8700个）与爬取的160+区县数据（497个）推算一致
   - 校验结果证实爬取数据的可行性（占全国区县8%的样本代表性）

---

### 问题2：CFPS样本区县异常
**审稿意见：**  
CFPS基线仅覆盖160+县区，但论文使用651个县区数据。若因样本迁移导致，则迁移样本量少且自选择性强，不适合分析。

**作者回复：**
1. **异常样本分析**  
   - 筛选2016/2018/2020年迁移样本：  
     | 年份 | 基线区县数 | 其他区县数 | 其他区县样本量 | 占比 |
     |------|------------|------------|----------------|------|
     | 2016 | 162        | 59         | 218            | 1.1% |
   - 结论：迁移样本占比低（1.1%）且高度自选择

2. **模型修正**  
   - 删除迁移样本后重新回归（结果见<表4>）：
     - 医联体建设系数显著为正（列1-2）
     - Bartik工具变量法验证稳健性（列3,6）

---

### 问题3：CFPS与爬取数据匹配方法
**审稿意见：**  
CFPS不公布县区代码，如何匹配数据？

**作者回复：**
- 通过"中国家庭追踪调查一般限制性数据"线上申请获取保密数据
- 需在指定保密机室处理数据（<图3>申请界面截图）
- 因保密要求未展示详细申请记录（<图4>）

---

### 问题4：基层就医比例构建方法
**审稿意见：**  
分母应为有就医行为的样本总数，而非全体农民样本数。

**作者回复：**
1. **指标重构**  
   - **基层就医比例**：  
     `= 基层就医人数 / 总就诊人数`  
     （清洗无就医行为样本）
   - **基层医疗消费占比**：  
     `= 基层医疗消费额 / 总医疗消费额`

2. **补充分析**  
   - 检验医联体对总就诊规模的影响（结果见<表5>）：
     - 显著促进基层就诊规模
     - 对县级医院影响不显著
   - 新增文献支持：段晖(2020)、封进(2022)等

---

### 问题5：聚类层面定义
**审稿意见：**  
"聚类到地区层面"是否指县区层面？

**作者回复：**
- 确认聚类层面为**区县层面**
- 依据：
  1. 解释变量/被解释变量均在区县层面衡量
  2. 参考谢泽宇(2023)、毛其淋(2023)等文献
- 文本统一修改：
  - "地区固定效应" → "区县固定效应"
  - "时间固定效应" → "年份固定效应"

---

### 问题6：基层医疗机构信誉的解释
**审稿意见：**  
"农民患病严重仍选择基层就医反映信誉高"是否应解释为服务能力高？

**作者回复：**
**信誉与服务能力的区分依据：**
1. **信誉定义**  
   - 履行健康保障承诺获得的社会信任（社会学+经济学视角）
   - 在信息不对称下主导患者主观选择（靳卫东2024b）

2. **衡量方法差异**  
   - **服务能力**：通过`就医选择`×`医疗水平评价`交互项衡量
   - **信誉**：通过`病情严重程度`×`医疗机构选择`交互项衡量

3. **理论支持**  
   - 患者无法准确识别服务能力（周小梅2020）
   - 病情与机构选择错配反映信誉问题（王淑云2021）

---

## 专家二意见回复

### 问题1：核心解释变量度量
**审稿意见：**  
① 关键词"医联体+签约"未涵盖医共体；② 时点数据如何赋值三年面板；③ 应使用"是否建立医联体"而非数量。

**作者回复：**
1. **关键词优化与医共体控制**  
   - 新增爬取`医共体+签约`数据
   - 构建控制变量`是否建立医共体`（结果见<表6>）

2. **面板数据赋值方法**  
   - 每年末爬取存量值（如2018年数据=截至2017.12.31数量）
   - 反映政策执行动态性（包含新建/撤销案例）

3. **变量形式补充**  
   - 新增虚拟变量`是否建立医联体`进行稳健性检验（结果见<表8>）
   - 保留连续变量依据：
     - 零值样本仅占22.6%（<图5>核密度曲线）
     - 2017年后政策推进使数量分布合理（<表7>年度分布）

---

### 问题2：计量模型修正
**审稿意见：**  
① 模型应设在个人层面；② 统一固定效应术语；③ 删除无效工具变量。

**作者回复：**
1. **模型层级调整**  
   - 补充**个人层面**回归（结果见<表12>）：
     - 被解释变量：个体就医选择/基层消费额
     - 控制变量：性别/年龄/健康状况等微观指标
   - 保留区县层面分析理由：
     - 符合医疗消费下沉的宏观研究目标
     - 参考封进(2022)等文献的加总方法

2. **术语统一**  
   - "地区固定效应" → "区县固定效应"
   - "时间固定效应" → "年份固定效应"

3. **工具变量替换**  
   - 删除同省份均值工具变量（江艇教授指出内生性问题）
   - 采用**Bartik工具变量**：
     - 构造：`省其他区县医联体初始值 × 全国医联体增长率`
     - 结果见<表13>，通过相关性/排他性检验
     - 文献支持：刘诚(2023)、易行健(2018)

---

### 问题3：深化对医联体的认识
**审稿意见：**  
参考朱夫(2017)、杜创(2016)、付明卫(2022)解释分级诊疗未好转的原因。

**作者回复：**
**关键修改：**
1. **引言与理论分析**  
   - 补充收入水平对就医选择的影响（杜创2016）
   - 强调紧密型医联体"人财物一体化"机制（朱夫2017）

2. **政策建议**  
   - 新增三条建议：
     - 建立医院协同利益机制（杜创2016）
     - 提高基层"造血功能"+医师下沉激励（朱夫2017）
     - 实施医疗信息披露制度（付明卫2022）

---

## 总结
再次衷心感谢审稿专家和编辑部的细致工作！上述修改已全面提升论文质量，修改内容在稿件中通过**红色字体**标注。恳请继续指导！
