---
title: 英美隨機死亡率模型之量化比較研究 (A quantitative comparison of stochastic mortality models using data from England & Wales and the United States)
aliases: [Cairns 2007, Cairns 2009, M1-M8 Comparison]
authors: [Andrew J. G. Cairns, David Blake, Kevin Dowd, Guy D. Coughlan, David Epstein, Alen Ong, Igor Balevich]
year: 2007
institution: [英國赫瑞-瓦特大學, 倫敦城市大學卡斯商學院, 諾丁漢大學, 摩根大通 (J.P. Morgan LifeMetrics)]
journal: North American Actuarial Journal, 13(1), 1–35 (2009) / Discussion Paper PI-0701 (2007)
category: 隨機死亡率模型 / 模型評估與比較 / 長壽風險
tags: [actuarial-science, stochastic-mortality, model-comparison, lee-carter, cbd-model, bic, cohort-effect, robustness]
source_pdf: raw/papers/2007_cairns_comparison_stochastic.pdf
doi: 10.1080/10920277.2009.10597538
status: ingested
date: 2026-11-23
---

# 英美隨機死亡率模型之量化比較研究 (A quantitative comparison of stochastic mortality models using data from England & Wales and the United States)

> **論文出處**：*North American Actuarial Journal*, 13(1), 1–35 (2009) / Pensions Institute Discussion Paper PI-0701. DOI: [10.1080/10920277.2009.10597538](https://doi.org/10.1080/10920277.2009.10597538)  
> **作者**：Andrew J. G. Cairns, David Blake, Kevin Dowd, Guy D. Coughlan, David Epstein, Alen Ong, Igor Balevich  
> **本機存檔**：`raw/papers/2007_cairns_comparison_stochastic.pdf`

---

## 一、 研究背景與核心問題意識 (Motivation & Problem Statement)

自 1990 年代初李-卡特模型問世以來，學界相繼提出了數十種隨機死亡率模型變體（涵蓋雙線性模型、世代模型、P-splines 平滑模型、羅吉斯雙因子 CBD 模型等）。然而，**整個精算學界長期缺乏一套系統化、跨國別、以嚴謹統計指標與穩健性為依歸的橫向基準評測**。

精算師與養老金經理人面對海量模型時面臨巨大困惑：
- 究竟哪一種模型在擬合優度 (Goodness-of-fit) 與預測穩健性 (Robustness) 之間取得了最佳平衡？
- 世代效應 (Cohort Effect) 是否普遍存在，還是只存在於特定國家？
- 模型參數在不同的歷史數據區間下是否具備時間穩定性？

---

## 二、 核心方法與技術架構 (Methodology & Architecture)

### 1. 八大代表性隨機死亡率模型量化體系 (M1 ~ M8)
作者將當時學界主流模型歸納為同一套標準數學框架：

| 編號 | 模型簡稱與提出者 | 數學公式結構 | 模型哲學特徵 |
| :--- | :--- | :--- | :--- |
| **M1** | [[李-卡特模型 (Lee-Carter Model)]] (1992) | $\ln m(t,x) = \beta_x^{(1)} + \beta_x^{(2)} \kappa_t^{(2)}$ | 單一時期因子，年齡效應高度彈性 |
| **M2** | [[2006-renshaw-haberman-cohort]] (RH, 2006) | $\ln m(t,x) = \beta_x^{(1)} + \beta_x^{(2)} \kappa_t^{(2)} + \beta_x^{(3)} \gamma_{t-x}^{(3)}$ | LC 加裝世代效應，全雙線性 |
| **M3** | 年齡-時期-世代模型 (APC, Currie 2006) | $\ln m(t,x) = \beta_x^{(1)} + \kappa_t^{(2)} + \gamma_{t-x}^{(3)}$ | 加法型無加權，簡化版 M2 |
| **M4** | 二維懲罰仿樣模型 (P-splines, Currie 2004) | $\ln m(t,x) = \sum_{i,j} \theta_{ij} B_{ij}^{ay}(x, t)$ | 假設死亡率曲面絕對平滑 |
| **M5** | [[2006-cairns-two-factor-cbd]] (CBD 原始版) | $\text{logit}\, q(t,x) = \kappa_t^{(1)} + \kappa_t^{(2)} (x - \bar{x})$ | 雙因子（水平+斜率），無世代 |
| **M6** | CBD 世代擴展版 (CBD + Cohort) | $\text{logit}\, q(t,x) = \kappa_t^{(1)} + \kappa_t^{(2)} (x - \bar{x}) + \gamma_{t-x}^{(3)}$ | M5 加裝固定權重世代項 |
| **M7** | **CBD 二次年齡項版 (CBD Quadratic)** | $\text{logit}\, q(t,x) = \kappa_t^{(1)} + \kappa_t^{(2)} (x - \bar{x}) + \kappa_t^{(3)} ((x - \bar{x})^2 - \widehat{\sigma}_x^2) + \gamma_{t-x}^{(4)}$ | **引入二次曲率項捕捉高齡非線性** |
| **M8** | CBD 世代遞減版 (CBD Diminishing Cohort) | $\text{logit}\, q(t,x) = \kappa_t^{(1)} + \kappa_t^{(2)} (x - \bar{x}) + \gamma_{t-x}^{(3)} (x_c - x)$ | 世代影響隨年齡增長而衰減 |

### 2. 評測標準體系
1. **質化準則**：實作難易度、精簡性 (Parsimony)、透明度、樣本路徑生成能力、百分位數估計能力、參數風險納入能力、非平庸相關結構 (Non-trivial Correlation)。
2. **量化準則**：
   - 貝氏資訊準則 (BIC)：$BIC_r = l(\widehat{\phi}_r) - \frac{1}{2} \nu_r \ln N$，平衡概似值與參數自由度懲罰。
   - 概似比檢定 (Likelihood Ratio Test, LRT)：檢驗巢狀模型（如 M1 vs M2、M5 vs M6 vs M7）參數擴充是否顯著。
   - 標準化殘差圖檢驗：檢定 i.i.d. 獨立同分佈性。
   - **參數估計之穩健性 (Robustness)**：比對全區間與縮減歷史區間之參數漂移。

---

## 三、 關鍵實驗成果與評測基準 (Empirical Results & Benchmarks)

### 1. 英美兩國 BIC 排行榜
以 60–89 歲高齡男性人口數據進行擬合：
- **英國 (England & Wales, 1961–2004)**：
  - **冠軍：M8 (BIC = -8396.8)**，其次為 **M7 (BIC = -8421.1)**，第三為 M2 (-8458.1)。
  - 結論：英國數據存在極為強烈且無可爭辯的**世代效應**（LRT 檢定以 $p < 0.000001$ 徹底否決無世代效應的 M1 與 M5）。
- **美國 (United States, 1968–2003)**：
  - **表面冠軍：M2 (BIC = -10383.2)**，其次為 **M7 (BIC = -12218.9)**。
  - 結論：美國高齡層的世代效應遠弱於英國，但其死亡率 Logit 曲線隨年齡展現了顯著的**二次彎曲 (Quadratic Curvature)**。

### 2. 參數穩健性審查 (The Fatal Flaw of M2)
當作者將估計區間縮減至 1980/1981 以後時：
- **M2 (Renshaw-Haberman) 徹底崩潰**：參數 $\beta_x^{(2)}, \beta_x^{(3)}, \gamma_{t-x}$ 出現劇烈震盪與跳躍，證實 M2 具有多重局部極值與假性過擬合。
- **M7 (CBD Quadratic) 表現出無與倫比的參數穩定性**：無論數據區間如何變動，M7 的四組參數曲線幾乎完全重疊！

> **核心結論**：若兼顧統計擬合度與實務預測的穩健性，**Model M7 是英美兩國最推薦的綜合首選模型**。

---

## 四、 侷限性與批判性反思 (Limitations & Critical Review)

1. **僅針對 60–89 歲高齡群**：CBD 家族（M5~M8）嚴重依賴羅吉斯線性/二次假設，完全無法擬合 20~50 歲的青少年死亡高峰。
2. **暴露人年數據品質問題**：美國數據殘差變異數高達 7.5~11.5，反映官方人口暴露數估計存在顯著雜訊。

---

## 五、 文獻脈絡與演進關係 (Lineage & Related Work)

- **承接自**：Lee & Carter (1992)、Brouhns et al. (2002)、Renshaw & Haberman (2006)、Cairns et al. (2006b)。
- **後續影響**：本文被譽為隨機死亡率模型領域的「天書與標準字典」，所定義的 **M1~M8 編號**成為後續十餘年間所有死亡率建模論文（包括 Plat 2009、O'Hare & Li 2012、Bjerre 2022）引用的通用標準代號。
- **跨論文深度對比**：收錄於 [[隨機死亡率模型與機器學習技術演進對比統整]]，呈現八大模型與現代機器學習/深度學習之全面橫向對比。
