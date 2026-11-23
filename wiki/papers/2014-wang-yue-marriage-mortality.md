---
title: 婚姻、健康與死亡率：基於臺灣人口數據之研究 (Mortality, Health, and Marriage - A Study Based on Taiwan's Population Data)
aliases: [Wang & Yue 2014, 婚姻與死亡率, Taiwan Marital Mortality]
authors: [王信忠, 余清祥 (Jack C. Yue)]
year: 2014
institution: [真理大學統計與精算學系, 國立政治大學統計學系]
journal: Society of Actuaries Living to 100 Monograph (2014) / North American Actuarial Journal (2015)
category: 精算人口學 / 死亡率異質性 / 婚姻狀態與核保風險因子
tags: [actuarial-science, demography, marital-status, mortality-differentials, underwriting, taiwan-population, lee-carter]
source_pdf: raw/papers/2014_wang_yue_marriage_mortality.pdf
status: ingested
date: 2026-11-23
---

# 婚姻、健康與死亡率：基於臺灣人口數據之研究 (Mortality, Health, and Marriage: A Study Based on Taiwan's Population Data)

> **論文出處**：*Society of Actuaries (SOA) Living to 100 Monograph*, 2014 / *North American Actuarial Journal*, 2015  
> **作者**：王信忠 (Hsin-Chung Wang)、余清祥 (Jack C. Yue)  
> **本機存檔**：`raw/papers/2014_wang_yue_marriage_mortality.pdf`

---

## 一、 研究背景與核心問題意識 (Motivation & Problem Statement)

### 1. 傳統精算死亡率模型的共變異數盲區
以 [[李-卡特模型 (Lee-Carter Model)]] 與 CBD 家族為首的主流精算模型，僅考慮年齡 ($x$)、年份 ($t$) 與性別三個維度。然而在人口學與流行病學領域，社經地位、教育水準與**婚姻狀態（Marital Status）**對人類壽命具有極其深遠的影響。

### 2. 臺灣社會婚姻結構劇變的衝擊
自 1980 年代以來，臺灣面臨未婚率劇增、初婚年齡大幅延後與離婚率飆升的結構轉變。精算界亟需探討：
- 婚姻狀態是否在統計上對死亡率改善軌跡構成顯著的異質性？
- 婚姻帶來的死亡率差異幅度，是否足以達到商業保險與退休年金作為「核保與定價風險因子 (Rating Factor)」的實質標準？

---

## 二、 核心方法與技術架構 (Methodology & Architecture)

### 1. 數據分組與婚姻狀態劃分
依據臺灣內政部戶政司歷史人口與死亡登記檔案，將 20 歲以上人口依性別嚴格劃分為四大婚姻群體：
1. **未婚 (Single / Never Married)**
2. **有偶 (Married)**
3. **離婚 (Divorced)**
4. **喪偶 (Widowed)**

### 2. 分組隨機死亡率模型設定
對不同婚姻狀態 $s \in \{\text{Single, Married, Divorced, Widowed}\}$ 分別擬合卜瓦松對數雙線性模型：
$$\ln \mu_{x,t,s} = \alpha_{x,s} + \beta_{x,s} \kappa_{t,s} + \epsilon_{x,t,s}$$
並透過風險比值（Hazard Ratio, HR）與死亡率倍數比較其相對於「有偶群體」的額外死亡風險：
$$\text{Relative Mortality}_{x,s} = \frac{\mu_{x,t,s}}{\mu_{x,t, \text{Married}}}$$

---

## 三、 關鍵實驗成果與評測基準 (Empirical Results & Benchmarks)

1. **實證數據覆蓋**：臺灣 1974–2011 年全國人口與死亡註冊大數據。
2. **婚姻保護效應（Marriage Protection）的量化**：
   - 實證顯示，**「有偶人口」在所有年齡層中均享有最低的死亡率**，無論男女皆然。
   - 死亡風險排序呈現一致性定律：**有偶 < 未婚 < 喪偶 < 離婚**。
   - **離婚男性面臨最嚴峻的死亡懲罰**：在 35–55 歲壯年段，離婚男性的死亡率為有偶男性的 **2.5 倍至 3.2 倍**，主要死因集中於意外、自殺、心血管疾病與肝硬化。
3. **震驚精算界的實證結論：超越吸菸差異**：
   - 作者將婚姻死亡率差異與傳統精算核保最具指標性的「吸菸者 vs. 非吸菸者」進行橫向對比；
   - **實證發現：在特定年齡段（特別是 30–50 歲男性），「離婚 vs. 有偶」的死亡率倍數差距，竟然顯著大於「吸菸 vs. 不吸菸」的死亡率倍數！**
   - 這證明婚姻狀態具備高度統計顯著性與經濟實質性，可作為年金長壽風險細分或人壽保險差異化定價的重要參考指標。

---

## 四、 侷限性與批判性反思 (Limitations & Critical Review)

1. **因果關係與健康選擇效應 (Selection vs. Protection)**：
   - 本研究無法完全排除「健康選擇假說」（即身體原本就較健康、經濟條件較佳者較容易維持婚姻，而罹患慢性病或失業者較容易離婚或無法結婚）帶來的反向因果偏誤。
2. **保險監理與法規倫理障礙**：
   - 儘管精算數據高度顯著，但在人壽保險核保中直接以「婚姻狀態」作為差別費率因子，可能面臨性別平權與人權法規的公眾質疑。

---

## 五、 文獻脈絡與演進關係 (Lineage & Related Work)

- **承接自**：[[2003-yue-taiwan-fertility]]、Hu & Goldman (1990) 婚姻死亡率理論、[[李-卡特模型 (Lee-Carter Model)]]。
- **與機器學習特徵工程的呼應**：
  - 本文的實證發現為現代機器學習死亡率模型（如 [[2022-tree-based-mortality]] 與 [[2024-qiao-wang-ml-long-term-mortality]]）納入跨領域異質性共變異數提供了強大的實證背書。
- **跨論文深度對比**：收錄於 [[隨機死亡率模型與機器學習技術演進對比統整]]。
