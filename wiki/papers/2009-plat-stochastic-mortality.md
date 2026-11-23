---
title: 隨機死亡率建模評估與統一架構 (On stochastic mortality modeling)
aliases: [Plat 2009, Plat Model, Model M9]
authors: [Richard Plat]
year: 2009
institution: [荷蘭阿姆斯特丹大學 (University of Amsterdam), Eureko / Achmea]
journal: Insurance: Mathematics and Economics, 45(3), 393–404
category: 隨機死亡率模型 / 全年齡 GAPC / 長壽風險避險
tags: [actuarial-science, stochastic-mortality, plat-model, m9, gapc, cohort-effect, longevity-risk, full-age-range]
source_pdf: raw/papers/2009_plat_stochastic_mortality.pdf
doi: 10.1016/j.insmatheco.2009.08.006
status: ingested
date: 2026-11-23
---

# 隨機死亡率建模評估與統一架構 (On stochastic mortality modeling)

> **論文出處**：*Insurance: Mathematics and Economics*, 45(3), 393–404 (2009). DOI: [10.1016/j.insmatheco.2009.08.006](https://doi.org/10.1016/j.insmatheco.2009.08.006)  
> **作者**：Richard Plat  
> **本機存檔**：`raw/papers/2009_plat_stochastic_mortality.pdf`

---

## 一、 研究背景與核心問題意識 (Motivation & Problem Statement)

### 1. 既有隨機死亡率模型之割裂與兩難
在 2000 年代後期，精算學界面臨兩大主流模型各執一端的局面：
1. **李-卡特體系 (Lee-Carter / M1, Renshaw-Haberman / M2)**：
   - 優點：涵蓋全年齡段（0 至 90+ 歲）。
   - 致命缺陷：M1 無法捕捉世代效應，且所有年齡的改善均由單一因子驅動（相關係數為 1 的平凡結構）；M2 雖引入世代因子，但概似函數具備多峰性，估計極度不穩健、易於發散。
2. **CBD 體系 (Cairns-Blake-Dowd / M5–M8)**：
   - 優點：參數精簡、無參數可辨識性問題、年齡相關結構靈活。
   - 致命缺陷：**僅適用於 60 歲以上退休高齡人口**，在 60 歲以下因缺少靜態年齡輪廓與無法擬合意外凸起而完全失效。

### 2. 本文的研究動機
保險公司同時經營**壽險（全年齡、過早死亡風險）**與**年金/退休金（高齡、長壽風險）**，迫切需要一個**兼具 CBD 參數穩健性與 Lee-Carter 全年齡適用性，同時能捕捉世代效應與非平凡年齡相關性**的統一模型（即精算界著名的 **Model M9**）。

---

## 二、 核心方法與技術架構 (Methodology & Architecture)

### 1. Plat 模型 (Model M9) 的數學結構
對數死亡力 $\ln \mu_{x,t}$ 表述為：
$$\ln \mu_{x,t} = \alpha_x + \kappa_t^{(1)} + \kappa_t^{(2)} (\bar{x} - x) + \kappa_t^{(3)} (\bar{x} - x)^+ + \gamma_{t-x} + \epsilon_{x,t}$$
其中：
- $\alpha_x$：基礎年齡輪廓（Baseline Age Profile）。
- $\kappa_t^{(1)}$：整體死亡率改善的水平因子（Level Effect，影響全年齡）。
- $\kappa_t^{(2)}$：死亡率改善的斜率因子（Slope Effect，影響中高齡）。
- $\kappa_t^{(3)}$：幼年與年輕人口特徵調節因子，$(\bar{x} - x)^+ = \max(\bar{x} - x, 0)$ 為分段折線鉸鏈函數（Hinge Function）。
- $\gamma_{t-x}$：出生世代因子（Cohort Effect，出生年 $c = t - x$）。
- $\bar{x}$：預設的轉折年齡錨點（通常取全體樣本年齡之中位數或平均值，如 65 歲）。

### 2. 參數唯一可識別性約束 (Identifiability Constraints)
為了確保極大概似估計解唯一：
$$\sum_t \kappa_t^{(1)} = 0, \quad \sum_t \kappa_t^{(2)} = 0, \quad \sum_t \kappa_t^{(3)} = 0$$
$$\sum_c \gamma_c = 0, \quad \sum_c c \gamma_c = 0$$

### 3. 動態外推與風險中性定價擴展
- **實體機率空間 ($P$)**：時期向量 $\boldsymbol{\kappa}_t = (\kappa_t^{(1)}, \kappa_t^{(2)}, \kappa_t^{(3)})^T$ 擬合三變量隨機游走漂移過程 (MRWD)，世代因子 $\gamma_c$ 擬合單變量 $\text{ARIMA}(1,1,0)$。
- **風險中性定價 ($Q$)**：作者進一步透過市場長壽風險溢酬（Market Price of Longevity Risk）將模型推廣至無套利金融架構，可用於長壽債券 (Longevity Bonds) 與交換合約之衍生品定價。

---

## 三、 關鍵實驗成果與評測基準 (Empirical Results & Benchmarks)

1. **實證數據集**：美國、英格蘭及威爾斯、荷蘭三國男性歷史人口死亡數據（1950–2005，年齡 0–89 歲）。
2. **模型選擇與擬合指標 (BIC)**：
   - 貝氏資訊準則 (BIC) 顯著優於 Lee-Carter 模型（M1）與單純 CBD 模型（M5）。
   - 殘差檢驗顯示，對角線世代相關殘差幾乎被完全消除。
3. **參數估計的穩健性檢驗 (Robustness Audit)**：
   - 將訓練時期自 1950–2005 縮減為 1960–2005 與 1970–2005，Plat 模型的參數形態與估計值保持高度一致，完全克服了 Renshaw-Haberman (M2) 對樣本時間長度極端敏感的弊病。

---

## 四、 侷限性與批判性反思 (Limitations & Critical Review)

1. **分段折線函數 $(\bar{x} - x)^+$ 的剛性與不可微性**：
   - 鉸鏈函數在臨界點 $\bar{x}$ 處存在斜率折角（Kink），在平滑的死亡率曲面上顯得過於生硬，進而引發了 [[2012-ohare-li-young-mortality]] 提出以光滑二次多項式取代的改良版（Model M10）。
2. **參數維度略高**：
   - 包含三個時期因子與一個世代因子，需要相對長跨度的歷史時間序列數據才能獲得穩定的共變異數矩陣。

---

## 五、 文獻脈絡與演進關係 (Lineage & Related Work)

- **承接自**：[[李-卡特模型 (Lee-Carter Model)]]、[[2002-brouhns-poisson-lc]]、[[2006-cairns-two-factor-cbd]]、[[2007-cairns-comparison-stochastic]]。
- **啟發與對標**：
  - 被譽為連結 Lee-Carter 與 CBD 兩大學派的里程碑，正式確立為 **Model M9**。
  - 直接促成了 [[2012-ohare-li-young-mortality]]（以二次平滑曲線優化本模型為 Model M10）。
  - 在機器學習領域，成為 [[2019-levantesi-pizzorusso-ml]] 殘差混合學習與 [[2022-tree-based-mortality]] 33 國長期回測中最核心的傳統精算對標基準之一。
- **跨論文深度對比**：收錄於 [[隨機死亡率模型與機器學習技術演進對比統整]]。
