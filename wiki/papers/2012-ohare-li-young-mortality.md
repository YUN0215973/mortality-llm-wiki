---
title: 解釋年輕族群死亡率：擴展 Plat 模型之非線性創新 (Explaining young mortality)
aliases: [O'Hare & Li 2012, O'Hare 2012, Model M10]
authors: [Colin O'Hare, Youwei Li]
year: 2012
institution: [英國貝爾法斯特女王大學管理學院 (Queen's University of Belfast)]
journal: Insurance: Mathematics and Economics, 50(1), 12–25
category: 隨機死亡率模型 / 全年齡建模 / 非線性效應
tags: [actuarial-science, stochastic-mortality, plat-model, young-mortality, accident-hump, m10-model, bic]
source_pdf: raw/papers/2012_ohare_li_young_mortality.pdf
doi: 10.1016/j.insmatheco.2011.09.005
status: ingested
date: 2026-11-23
---

# 解釋年輕族群死亡率：擴展 Plat 模型之非線性創新 (Explaining young mortality)

> **論文出處**：*Insurance: Mathematics and Economics*, 50(1), 12–25. DOI: [10.1016/j.insmatheco.2011.09.005](https://doi.org/10.1016/j.insmatheco.2011.09.005)  
> **作者**：Colin O'Hare, Youwei Li  
> **本機存檔**：`raw/papers/2012_ohare_li_young_mortality.pdf`

---

## 一、 研究背景與核心問題意識 (Motivation & Problem Statement)

### 1. 傳統模型對「年輕族群死亡率」的普遍漠視
在 2010 年前的大多數隨機死亡率文獻中，研究者基於養老金與年金產品的負債特性，絕大多數僅聚焦於 60 歲以上或 50 歲以上的高齡人口（如 [[2006-cairns-two-factor-cbd]]、[[2007-cairns-comparison-stochastic]] 的 M5~M8 模型）。

然而，將模型應用於更廣年齡區間（如 5–89 歲）時，現有模型全面面臨重大挑戰：
1. **青少年「生活型態意外突起 (Lifestyle & Accident Hump)」**：在 15–25 歲之間，由於交通事故、藥物濫用、意外與暴力，死亡率曲線會出現強烈非線性波峰，傳統線性年齡假設完全失效。
2. **最新世代效應的遺失**：若模型直接排除 20 歲以下人口，將完全喪失最近 20 年出生之新世代 (Recent Cohorts) 的寶貴死亡動態數據。
3. **Plat (2009) 模型的線性局限性**：雖然 Plat 提出了嘗試覆蓋全年齡的四因子模型（M9），但其針對低齡引入的折線項 $\kappa_t^{(3)}(\bar{x}-x)^+$ 仍為純線性，在 5–89 歲的全年齡擬合中誤差暴增超過一倍。

---

## 二、 核心方法與技術架構 (Methodology & Architecture)

### 1. 非線性低齡二次擴展模型 (Model M10)
作者在 Plat (2009) 模型與李-卡特、CBD 的基礎上，提出改進型四因子模型：

$$\ln m(t,x) = a_x + \kappa_t^{(1)} + \kappa_t^{(2)}(\bar{x}-x) + \kappa_t^{(3)} \left[ (\bar{x}-x)^+ + [(\bar{x}-x)^+]^2 \right] + \gamma_{t-x} + \epsilon_{x,t}$$

其中：
- $(\bar{x}-x)^+ = \max(\bar{x}-x, 0)$：僅作用於平均年齡以下（如 55 歲以下）的年輕與中年族群。
- **關鍵創新項 $[(\bar{x}-x)^+]^2$**：**引入二次非線性特徵**，成功賦予模型足夠的曲率彈性，以精準刻畫青少年意外死亡突起。
- $a_x$：基準年齡死亡輪廓。
- $\kappa_t^{(1)}$：整體死亡率水平改善因子（非定常隨機漫步）。
- $\kappa_t^{(2)}$：年齡斜率調節因子（定常均值回歸過程）。
- $\gamma_{t-x}$：世代效應因子（無趨勢均值回歸過程）。

### 2. 估計方法與約束條件
採用 [[2002-brouhns-poisson-lc]] 的卜瓦松最大概似估計架構 $D_{x,t} \sim \text{Poisson}(E_{x,t} m_{x,t})$。
為了消除模型辨識度冗餘 (Identifiability)，施加三項約束：
$$\sum_{c=c_0}^{c_1} \gamma_c = 0, \quad \sum_{c=c_0}^{c_1} c \gamma_c = 0, \quad \sum_t \kappa_t^{(3)} = 0$$

---

## 三、 關鍵實驗成果與評測基準 (Empirical Results & Benchmarks)

1. **跨國評測**：覆蓋全球 **7 個已開發國家**（英國、英格蘭與威爾斯、蘇格蘭、美國、荷蘭、澳洲、紐西蘭），歷史區間 1950–2006 年。
2. **三大年齡區間橫向對比 (MAPE 平均絕對百分比誤差)**：

| 評測年齡區間 | Plat 模型 (M9) | 本文模型 (M10) | 核心差異 |
| :--- | :--- | :--- | :--- |
| **5–89 歲 (全年齡)** | 英國: 7.56% / 美國: 5.65% | **英國: 5.88% / 美國: 4.14%** | **全體 7 國全面大幅勝出，擬合誤差大幅降低** |
| **20–89 歲 (成年段)** | 英國: 3.27% / 美國: 2.76% | **英國: 2.77% / 美國: 2.31%** | 依然全面優於 Plat 模型 |
| **50–89 歲 (高齡段)** | 英國: 1.36% / 美國: 1.41% | **英國: 1.29% / 美國: 1.35%** | 保持高齡段頂尖表現 |

3. **參數穩定性與回測 (Backtesting)**：
   - 相比於 Renshaw-Haberman (M2) 的嚴重不穩定，M10 模型在 1975–2006 縮減區間下參數特徵高度一致，展現了優異的參數穩健性。

---

## 四、 侷限性與批判性反思 (Limitations & Critical Review)

1. **生活型態死亡的結構性外推風險**：年輕族群的意外死亡率受政策（如酒駕法規、禁菸政策、安全帶法）、醫療技術進展與流行病影響深遠，純粹依賴時間序列 ARIMA 外推仍有無法預測結構驟變的限制。
2. **二次項係數的固定性**：作者在研究中將二次項係數固定為 $a=1$，雖簡化了結構，但在特定國家可能存在更優的非整數曲率配置。

---

## 五、 文獻脈絡與演進關係 (Lineage & Related Work)

- **承接自**：[[李-卡特模型 (Lee-Carter Model)]]、[[2002-brouhns-poisson-lc]]、[[2006-cairns-two-factor-cbd]]、Plat (2009)。
- **架構地位**：成功填補了 CBD 家族無法處理全年齡的空白，建立了經典參數化模型能兼顧全年齡與世代效應的最高代表作（Model M10）。
- **跨論文深度對比**：收錄於 [[隨機死亡率模型與機器學習技術演進對比統整]]，探討全年齡參數化結構與純機器學習非參數結構之優劣。
