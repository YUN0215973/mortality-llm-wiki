---
title: 折扣數列模型 (Discount Sequence Model, DS 與 DSW)
aliases: [Discount Sequence Model, DS Model, DSW Model, 規律折扣數列模型, 折扣數列比值韋伯模型]
category: 精算人口學 / 高齡死亡率模型 / 關係模型
tags: [actuarial-science, old-age-mortality, relational-models, discount-sequence, dsw, weibull, longevity-risk]
date: 2026-11-23
---

# 折扣數列模型 (Discount Sequence Model, DS 與 DSW)

> **定義**：折扣數列模型（DS 模型）及其擴展架構「折扣數列比值韋伯模型（DSW 模型）」，是由臺灣精算與統計學者王信忠與余清祥（Wang & Yue, 2011, 2016）所開創之高齡死亡率關係模型。該模型將應用數學中「多臂吃角子老虎機問題（Multi-Armed Bandit Problem）」的規律折扣數列理論引進人口學，並結合工程可靠度韋伯分佈（Weibull Distribution），專門用於平滑與預測 65 歲至 105 歲超高齡人口之剩餘平均餘命與死亡率。

---

## 一、 核心數學理論與人口學映射

### 1. 規律折扣數列的定義
在隨機動態規劃中，數列 $\{a_n\}_{n=1}^\infty$ 若滿足 $a_n \in (0,1)$ 且其跨期折現比率具備特定單調性，稱為規律折扣數列。  
王信忠與余清祥將此概念對映至生命表（Life Table）：
- 設 $e_x$ 為 $x$ 歲人口之剩餘平均餘命（Life Expectancy），$l_x$ 為存活人數，$T_x = \sum_{k=0}^\infty L_{x+k}$ 為累積生存人年數。
- 定義**折扣數列比值因子 (Discount Sequence Ratio, $d_x$)**：
  $$d_x = \frac{e_{x+1}}{1 + e_x} = \frac{T_{x+1} / l_{x+1}}{1 + T_x / l_x}$$

### 2. 經典死亡率假說的統攝定理
作者於 2011 年發表之論文中嚴謹推導證明：**精算科學中所有經典的高齡死亡率假說，在數學本質上均為規律折扣數列的特例**：
1. **均勻死亡假設 (UDD)**：$d_x$ 嚴格單調遞減並收斂。
2. **定死力假設 (Constant Force)**：$d_x$ 為常數。
3. **雙曲線假設 (Hyperbolic)**：$d_x$ 滿足特定有理分式。
4. **岡珀茨定律 (Gompertz Law)**：$d_x$ 呈現穩定的非線性收斂軌跡。

---

## 二、 DSW 模型結構 (Discount Sequence Weibull)

為了精確描繪高齡族群（80 歲以上）普遍存在的「死亡率減速（Mortality Deceleration）」現象，作者導入可靠度工程中專門描述設備磨損老化的**韋伯分佈 (Weibull Distribution)**：
$$d_x = \exp\left\{ - \left( \frac{x - x_0}{\lambda} \right)^k \right\}$$
其中：
- $x_0$：高齡起始基準年齡（通常取 65 歲或 80 歲）。
- $\lambda > 0$：尺度參數（Scale Parameter）。
- $k > 0$：形狀參數（Shape Parameter），當 $k > 1$ 時表示老化速率隨年齡加速。

### 隨機化動態擴充 (Stochastic Dynamics)
為了進行跨年份長期預測，將參數視為隨時間演進的隨機過程，採用布朗運動隨機微分方程 (SDE) 進行蒙地卡羅情境模擬：
$$d \lambda_t = \theta (\mu - \lambda_t) dt + \sigma d W_t$$

---

## 三、 實證優勢與模型比較

在 [[2011-wang-yue-discount-sequence]] 與 [[2016-wang-yue-old-age-mortality]] 跨越臺灣、日本與美國 HMD 數據之大規模評測中：
1. **抗雜訊能力強**：超高齡數據（90 歲以上）暴露人年極小，粗死亡率呈劇烈鋸齒狀；DSW 透過剩餘餘命的積分轉換，天然過濾了離散雜訊。
2. **超越傳統關係模型**：樣本外滾動預測（Cross-Validation）精確度顯著超越 Gompertz 與 Coale-Kisker (1990) 模型。
3. **媲美複雜隨機模型**：在預測高齡平均餘命時，參數量極少的 DSW 模型的表現與 Lee-Carter 及 Cairns CBD 旗鼓相當，且徹底免除了 Renshaw-Haberman (M2) 嚴重的數值不收斂問題。

---

## 四、 相關文獻與交叉引用

- [[2011-wang-yue-discount-sequence]]：首度正式提出規律折扣數列與 DSW 模型的開山論文。
- [[2016-wang-yue-old-age-mortality]]：將 DSW 模型與台美日三國六大經典模型進行全面橫向比較。
- [[2006-cairns-two-factor-cbd]]：高齡專用隨機死亡率模型對標代表。
- [[通用年齡-時期-世代模型 (GAPC)]]：高齡隨機模型體系。
- [[長壽風險 (Longevity Risk)]]：高齡死亡率建模最核心之精算應用背景。
