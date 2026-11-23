---
title: 死亡率模型之比較：以臺灣資料為例 (A Comparison of Mortality Models - Evidence from Taiwan)
aliases: [Lee, Liu & Kung 2019, 臺灣死亡率模型比較, Taiwan Mortality Models Comparison]
authors: [李永琮, 劉議謙, 宮可倫]
year: 2019
institution: [國立嘉義大學財務金融學系, 國立臺中科技大學保險金融管理系, 逢甲大學風險管理與保險學系]
journal: 人口學刊, 58, 1–40
category: 隨機死亡率模型 / 模型比較 / 臺灣實證數據與非常態分佈
tags: [actuarial-science, stochastic-mortality, taiwan-population, model-comparison, plat-model, ohare-li, non-gaussian, nig-distribution, longevity-risk]
source_pdf: raw/papers/2019_lee_liu_taiwan_mortality_models.pdf
doi: 10.6191/JPS.201906_58.0001
status: ingested
date: 2026-11-23
---

# 死亡率模型之比較：以臺灣資料為例 (A Comparison of Mortality Models: Evidence from Taiwan)

> **論文出處**：*人口學刊* (Journal of Population Studies), 第 58 期, 頁 1–40 (2019年6月). DOI: [10.6191/JPS.201906_58.0001](https://doi.org/10.6191/JPS.201906_58.0001)  
> **作者**：李永琮 (Eng-Tsong Lee)、劉議謙 (I-Chien Liu)、宮可倫 (Ko-Lun Kung)  
> **本機存檔**：`raw/papers/2019_lee_liu_taiwan_mortality_models.pdf`

---

## 一、 研究背景與核心問題意識 (Motivation & Problem Statement)

### 1. 臺灣長壽風險加速與定價失真危機
隨著全民健保實施與醫療品質躍升，臺灣人口預期壽命持續創新高。保險公司若高估死亡率將導致壽險保費缺乏競爭力，若低估死亡率則將面臨嚴重的年金準備金提存不足（長壽風險）。

### 2. 西方文獻結論無法直接套用於臺灣
過去大型隨機死亡率模型比較（如 [[2007-cairns-comparison-stochastic|Cairns et al. 2007/2009]]、[[2009-plat-stochastic-mortality|Plat 2009]]）皆以歐美成熟人口為樣本。然而：
- 臺灣死亡率轉型時間短、改善速度比歐美更加劇烈；
- 傳統時間序列大多假設時期因子服從**常態分佈（高斯白雜訊）**，忽略了傳染病、天災或政策突變所引發的**厚尾（Fat Tails）與偏斜（Skewness）**特徵。
- 本文旨在針對臺灣 1970–2014 年本土數據進行最嚴謹的模型評比，並引進非常態跳躍創新分佈。

---

## 二、 核心方法與技術架構 (Methodology & Architecture)

### 1. 六大主流隨機死亡率模型比較架構
作者納入精算界六大經典與進階隨機模型：
1. **LC 模型**：[[李-卡特模型 (Lee-Carter Model)]] (1992)
2. **RH 模型**：[[2006-renshaw-haberman-cohort|Renshaw & Haberman (2006)]] 世代擴充
3. **Plat 模型**：[[2009-plat-stochastic-mortality|Plat (2009)]] 全年齡 M9 模型
4. **O'Hare-Li 模型**：[[2012-ohare-li-young-mortality|O'Hare & Li (2012)]] 二次多項式 M10 模型
5. **Mc-1 與 Mc-2 模型**：Mitchell et al. (2013) 針對高齡與青年死亡特徵的連續時間隨機變體

### 2. 非常態擾動分配擴充 (Non-Gaussian Innovation Distributions)
打破時期指數 $\kappa_t$ 僅服從標準高斯隨機游走的限制，引進三種廣義厚尾偏斜分佈：
- **常態反向高斯分配 (Normal Inverse Gaussian, NIG)**：能精確配適極端年份的長尾事件。
- **變異伽瑪分配 (Variance Gamma, VG)**：捕捉連續時間跳躍過程。
- **偏斜 t 分配 (Skewed Student's t)**：捕捉不對稱的肥尾衝擊。

---

## 三、 關鍵實驗成果與評測基準 (Empirical Results & Benchmarks)

1. **實證數據集**：人類死亡率資料庫 (HMD) 臺灣 1970–2014 年 20–89 歲男女分性別單齡死亡率。
2. **性別異質性評測發現**：
   - **男性資料**：由於受中年意外死因與特定時期生活型態波動干擾，結構最靈活的 **Mc-2 模型** 與 **[[2012-ohare-li-young-mortality|O'Hare-Li (M10)]]** 取得最佳的擬合度與樣本外預測精度。
   - **女性資料**：改善趨勢穩定且世代效應顯著，**[[2009-plat-stochastic-mortality|Plat (M9)]]** 與 **O'Hare-Li (M10)** 在 AIC、BIC 與 MAPE 上全面領先。
3. **非常態分配檢驗顯著勝出**：
   - 概似比檢定（Likelihood Ratio Test）證實：**NIG 與偏斜 t 分配顯著優於傳統常態分配**，證明臺灣死亡率改善序列具有顯著的厚尾風險，若以傳統高斯模型定價年金將低估巨災與長壽風險。

---

## 四、 侷限性與批判性反思 (Limitations & Critical Review)

1. **僅涵蓋國家層級總體人口數據**：
   - 本文使用的 HMD 數據代表臺灣全體國民，但商業保險年金保單的被保險人具有顯著的社會經濟篩選效應（社經地位高者壽命更長），直接套用可能產生基準風險（Basis Risk）。
2. **尚未納入現代機器學習演算法對標**：
   - 儘管引進了非常態分佈，但模型骨幹仍屬參數化 GAPC 範疇，未與隨機森林或深度序列模型進行交叉檢驗。

---

## 五、 文獻脈絡與演進關係 (Lineage & Related Work)

- **承接自**：[[2007-cairns-comparison-stochastic]]、[[2009-plat-stochastic-mortality]]、[[2012-ohare-li-young-mortality]]、Barndorff-Nielsen (1997) NIG 分配。
- **對照文獻**：與 [[2016-wang-yue-old-age-mortality]] 形成臺灣精算實證的雙璧，前者主攻高齡關係模型，本文則主攻全年齡隨機模型與非常態分佈。
- **跨論文深度對比**：收錄於 [[隨機死亡率模型與機器學習技術演進對比統整]]。
