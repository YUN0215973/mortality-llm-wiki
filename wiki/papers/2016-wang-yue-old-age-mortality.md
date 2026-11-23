---
title: 高齡死亡率模型的探討 (A Study on Old-Age Mortality Models)
aliases: [Wang, Yue & Chen 2016, 高齡死亡率模型探討, Old-Age Mortality Models Comparison]
authors: [王信忠, 余清祥 (Jack C. Yue), 陳怡萱]
year: 2016
institution: [真理大學統計與精算學系, 國立政治大學統計學系]
journal: 人口學刊, 52, 1–42
category: 高齡死亡率模型 / 關係模型與隨機模型大規模對比 / 交叉驗證
tags: [actuarial-science, old-age-mortality, dsw-model, gompertz, coale-kisker, lee-carter, cbd-model, model-comparison, cross-validation, taiwan-population]
source_pdf: raw/papers/2016_wang_yue_old_age_mortality.pdf
status: ingested
date: 2026-11-23
---

# 高齡死亡率模型的探討 (A Study on Old-Age Mortality Models)

> **論文出處**：*人口學刊* (Journal of Population Studies), 第 52 期, 頁 1–42 (2016年6月)  
> **作者**：王信忠、余清祥、陳怡萱  
> **本機存檔**：`raw/papers/2016_wang_yue_old_age_mortality.pdf`

---

## 一、 研究背景與核心問題意識 (Motivation & Problem Statement)

### 1. 超高齡社會來臨與年金長壽風險引爆
隨著臺灣、日本與全球步入高齡與超高齡社會，高齡人口（65 歲以上）特別是極高齡族群（85 歲至 105 歲）的死亡率與平均餘命預測，成為年金保險清償能力與政府社會安全基金的最核心變數。

### 2. 關係模型 vs. 隨機模型之學術爭鳴
精算與人口統計學界歷來分裂為兩大建模流派：
- **關係模型 (Relational Models)**：以 Gompertz (1825)、Coale & Kisker (1990) 以及王信忠與余清祥 (2011) 提出的 [[2011-wang-yue-discount-sequence|規律折扣數列比值韋伯模型 (DSW)]] 為代表，強調人口學生命律則與經驗曲線平滑。
- **隨機模型 (Stochastic Models)**：以 [[李-卡特模型 (Lee-Carter Model)]] (1992)、[[2006-renshaw-haberman-cohort|Renshaw-Haberman (2006)]] 與 [[2006-cairns-two-factor-cbd|CBD 模型 (2006)]] 為代表，強調時間序列動態外推與隨機波動區間。
- **核心待解問題**：在面對高齡數據的劇烈波動與樣本稀疏時，究竟哪一類模型在樣本外預測與跨國泛化能力上更具優勢？

---

## 二、 核心方法與技術架構 (Methodology & Architecture)

本文構建了精算文獻中罕見的六大模型跨流派橫向對比體系：

### 1. 受測之關係模型 (Relational Models)
1. **岡珀茨模型 (Gompertz Model)**：$\mu_x = B c^x$（死亡力隨年齡指數成長）。
2. **寇爾-基斯克模型 (Coale and Kisker, 1990)**：針對 85 歲以上高齡死亡率之對數成長率施加線性遞減約束：$k_x = k_{x-1} + s(x - 84)$。
3. **折扣數列比值韋伯模型 (DSW Model)**：王信忠與余清祥 (2011) 提出，以規律折扣數列結合工程可靠度韋伯分佈平滑剩餘壽命比值：$d_x = \exp\left\{ - \left(\frac{x - x_0}{\lambda}\right)^k \right\}$。

### 2. 受測之隨機死亡率模型 (Stochastic Models)
4. **李-卡特模型 (Lee-Carter / M1)**：$\ln m_{x,t} = \alpha_x + \beta_x \kappa_t$。
5. **倫蕭-哈伯曼模型 (Renshaw-Haberman / M2)**：納入世代因子 $\gamma_{t-x}$。
6. **CBD 模型 (Cairns-Blake-Dowd / M5)**：$\text{logit}\, q_{x,t} = \kappa_t^{(1)} + \kappa_t^{(2)} (x - \bar{x})$。

### 3. 評測標準與滾動交叉驗證 (Rolling Cross-Validation)
- 採用滾動窗口進行樣本外預測（Out-of-Sample Forecasting），評估指標包含均方根誤差 (RMSE)、平均絕對百分比誤差 (MAPE) 以及平均餘命 $e_{65}$ 與 $e_{85}$ 的預測偏誤。

---

## 三、 關鍵實驗成果與評測基準 (Empirical Results & Benchmarks)

1. **跨國數據集**：人類死亡率資料庫 (HMD) 中 **臺灣、日本與美國** 三國之 1970–2009 年單齡與五齡組高齡人口數據。
2. **核心實證評測結論**：
   - **實證結論 1（DSW 關係模型的優越性）**：本土學者提出的 **DSW 模型在三個國家的高齡樣本外預測中，表現不僅全面超越經典 Gompertz 與 Coale-Kisker，且預測精確度完全不遜於結構複雜的隨機模型（甚至在多數高齡組別優於 Lee-Carter）**。
   - **實證結論 2（CBD 模型在高齡隨機模型中奪冠）**：在隨機模型組中，專為高齡設計的 **CBD (M5)** 展現出最高的預測穩定度，呼應了 [[2007-cairns-comparison-stochastic]] 的國際評測結論。
   - **實證結論 3（Renshaw-Haberman 估計崩潰）**：納入世代因子的 M2 模型在高齡組再次出現嚴重的參數跳動與估計不穩定，證實不適合直接用於高齡長壽風險預測。

---

## 四、 侷限性與批判性反思 (Limitations & Critical Review)

1. **僅評測點預測，未延伸至分位數風險評估**：
   - 關係模型長於餘命的平滑點預測，但在歐盟 Solvency II 或台灣 ICS 資本要求下，隨機模型能提供完整的蒙地卡羅情境分佈，關係模型在此方面的隨機化擴展仍有待深化。
2. **未納入新興機器學習模型進行對標**：
   - 評測範圍聚焦於傳統參數與統計模型，尚未涵蓋當時剛萌芽的機器學習決策樹或自編碼器。

---

## 五、 文獻脈絡與演進關係 (Lineage & Related Work)

- **承接自**：[[2011-wang-yue-discount-sequence]]、[[2006-cairns-two-factor-cbd]]、[[2007-cairns-comparison-stochastic]]。
- **對標與啟發**：
  - 本文是臺灣本土人口與精算學者對國際高齡死亡率模型最完整的大規模橫向評測，為後續 [[2019-lee-liu-taiwan-mortality-models]]（臺灣全齡模型比較）奠定了堅實的實證參照。
- **跨論文深度對比**：收錄於 [[隨機死亡率模型與機器學習技術演進對比統整]]。
