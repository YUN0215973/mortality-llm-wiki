---
title: 規律折扣數列與高齡死亡率 (Regular Discount Sequences and Old-Age Mortality)
aliases: [Wang & Yue 2011, 折扣數列模型, DSW Model, Regular Discount Sequences]
authors: [王信忠, 余清祥 (Jack C. Yue)]
year: 2011
institution: [真理大學統計與精算學系, 國立政治大學統計學系]
journal: 人口學刊, 43, 1–38
category: 高齡死亡率模型 / 關係模型 / 隨機微分方程與工程可靠度
tags: [actuarial-science, old-age-mortality, discount-sequence, dsw-model, gompertz, weibull, longevity-risk, taiwan-population]
source_pdf: raw/papers/2011_wang_yue_discount_sequence.pdf
status: ingested
date: 2026-11-23
---

# 規律折扣數列與高齡死亡率 (Regular Discount Sequences and Old-Age Mortality)

> **論文出處**：*人口學刊* (Journal of Population Studies), 第 43 期, 頁 1–38 (2011年12月)  
> **作者**：王信忠 (Hsin-Chung Wang)、余清祥 (Jack C. Yue)  
> **本機存檔**：`raw/papers/2011_wang_yue_discount_sequence.pdf`

---

## 一、 研究背景與核心問題意識 (Motivation & Problem Statement)

### 1. 超高齡人口（80歲以上）建模的精算死角
隨著全球平均壽命不斷攀升，退休年金與長期照護保險最致命的「長壽風險 (Longevity Risk)」集中爆發於 **80 歲至 105 歲** 的極端高齡人口：
- **數據稀疏與雜訊劇烈**：超高齡存活人數極少，粗死亡率呈鋸齒狀劇烈跳動；
- **傳統模型的不適應**：經典隨機模型（如 [[李-卡特模型 (Lee-Carter Model)]]）在高齡組容易低估壽命延長速度；而經典參數模型（如 Gompertz、Coale-Kisker）則過度依賴剛性幾何假設，難以精確刻畫高齡死亡率減速（Mortality Deceleration）現象。

### 2. 本文的研究動機
跳脫傳統僅從純經驗公式修勻的角度，首度嘗試將應用數學與動態規劃中的**「吃角子老虎機問題（Multi-Armed Bandit Problem）之規律折扣數列（Regular Discount Sequences）」**概念引入人口精算，構建具備堅實數學理論的高齡死亡率模型。

---

## 二、 核心方法與技術架構 (Methodology & Architecture)

### 1. 規律折扣數列之人口學映射
在動態決策中，折扣因子序列衡量跨期價值折現。作者將其映射至生命表之存活人數 $l_x$ 與剩餘平均餘命 $e_x$：
- 定義折扣數列比值因子：
  $$d_x = \frac{e_{x+1}}{1 + e_x} = \frac{T_{x+1} / l_{x+1}}{1 + T_x / l_x}$$
- **理論證明**：作者於文中嚴謹推導證明，精算學中四種經典的死亡分佈假設：
  1. **均勻死亡假設 (Uniform Distribution of Deaths, UDD)**
  2. **定死力假設 (Constant Force of Mortality)**
  3. **雙曲線假設 (Hyperbolic Assumption)**
  4. **岡珀茨定律 (Gompertz Law)**  
  **在數學上均嚴格滿足「規律折扣數列」的單調性與收斂性條件**！這證明規律折扣數列是統攝經典壽命理論的一般化框架。

### 2. 折扣數列比值韋伯模型 (DSW Model)
為了捕捉高齡死亡率減速與老化特徵，作者結合工程可靠度理論中的韋伯分佈（Weibull Distribution），提出 **DSW 模型 (Discount Sequence Weibull)**：
$$d_x = \exp\left\{ - \left( \frac{x - x_0}{\lambda} \right)^k \right\}$$
其中 $x_0$ 為高齡起始年齡，$\lambda$ 為尺度參數，$k$ 為形狀參數。

### 3. 布朗運動隨機微分方程動態外推 (Stochastic Dynamic Modeling)
將時間趨勢納入，假設參數 $k_t$ 或 $d_{x,t}$ 隨時間服從幾何布朗運動（Geometric Brownian Motion）或均數復歸過程：
$$d X_t = \theta (\mu - X_t) dt + \sigma d W_t$$
藉由蒙地卡羅模擬（Monte Carlo Simulation）產出高齡餘命的隨機預測信賴區間。

---

## 三、 關鍵實驗成果與評測基準 (Empirical Results & Benchmarks)

1. **實證數據庫**：人類死亡率資料庫 (HMD) 中 **臺灣、日本與美國** 三國 1970–2007 年 65 歲以上男女人口死亡資料。
2. **交叉驗證 (Cross-Validation) 與模型對比**：
   - 與 Gompertz 模型、Lee-Carter 模型進行樣本外預測（Forecasting）均方根誤差比較。
   - **實證結論**：在 80 歲以上極高齡區間，**DSW 模型在三個國家的男女資料中，預測精確度與穩健性全面擊敗 Gompertz 與傳統隨機模型**，能平滑修復粗數據的雜訊，且有效避免外推時死亡率過度膨脹或萎縮。

---

## 四、 侷限性與批判性反思 (Limitations & Critical Review)

1. **僅適用於單調老化的中高齡群體 (65+)**：
   - 規律折扣數列建立在餘命單調遞減的假設上，無法套用於含有嬰幼兒死亡率驟降或青年意外死亡凸起的全年齡段（0–60 歲）。
2. **跨期隨機擾動項的估計負擔**：
   - 隨機微分方程的擴散項係數 $\sigma$ 估計對歷史區間長度較為敏感。

---

## 五、 文獻脈絡與演進關係 (Lineage & Related Work)

- **承接自**：Gompertz (1825)、Gittins (1989) 規律折扣數列理論、Coale & Kisker (1990)。
- **後續引領**：
  - 本文確立了 DSW 模型在高齡精算之地位，直接引領了後續 [[2016-wang-yue-old-age-mortality]] 對高齡隨機模型與關係模型的系統性大規模評測。
- **跨論文深度對比**：收錄於 [[隨機死亡率模型與機器學習技術演進對比統整]]。
