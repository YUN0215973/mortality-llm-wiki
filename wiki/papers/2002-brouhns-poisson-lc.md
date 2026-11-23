---
title: 卜瓦松對數雙線性迴歸於預測生命表構建之應用 (A Poisson log-bilinear regression approach to the construction of projected lifetables)
aliases: [Brouhns 2002, Poisson Lee-Carter, Poisson LC]
authors: [Natacha Brouhns, Michel Denuit, Jeroen K. Vermunt]
year: 2002
institution: [比利時法語天主教魯汶大學 (UCL), 荷蘭蒂爾堡大學 (Tilburg University)]
journal: Insurance: Mathematics and Economics, 31(3), 373–393
category: 隨機死亡率模型 / 廣義線性模型 / 參數估計
tags: [actuarial-science, stochastic-mortality, lee-carter, poisson-regression, maximum-likelihood, glm]
source_pdf: raw/papers/2002_brouhns_poisson_lc.pdf
doi: 10.1016/S0167-6687(02)00185-3
status: ingested
date: 2026-11-23
---

# 卜瓦松對數雙線性迴歸於預測生命表構建之應用 (A Poisson log-bilinear regression approach to the construction of projected lifetables)

> **論文出處**：*Insurance: Mathematics and Economics*, 31(3), 373–393. DOI: [10.1016/S0167-6687(02)00185-3](https://doi.org/10.1016/S0167-6687(02)00185-3)  
> **作者**：Natacha Brouhns, Michel Denuit, Jeroen K. Vermunt  
> **本機存檔**：`raw/papers/2002_brouhns_poisson_lc.pdf`

---

## 一、 研究背景與核心問題意識 (Motivation & Problem Statement)

### 1. 原始李-卡特模型 (Lee-Carter 1992) 的統計根本缺陷
原始 [[李-卡特模型 (Lee-Carter Model)]] 採用奇異值分解 (Singular Value Decomposition, SVD) 最小化對數死亡率的均方誤差：
$$\ln \widehat{m}_{x,t} = \alpha_x + \beta_x \kappa_t + \epsilon_{x,t}$$
這種最小平方法 (OLS/SVD) 隱含了一項致命假設：**殘差 $\epsilon_{x,t}$ 具有均齊變異數 (Homoskedasticity)**。

但在實際人口死亡數據中，**這項假設極度不符合現實**：
1. **高齡組樣本變異數暴增**：高齡族群暴露人年數（Exposures, $E_{x,t}$）極小，死亡人數波動劇烈，對數死亡率的變異數遠大於年輕族群（Heteroskedasticity）。
2. **總死亡人數無法吻合**：第一階段 SVD 擬合完成後，預測的死亡總人數與實際觀察死亡人數不符，必須藉由第二階段強行非線性數值搜尋重調 $\kappa_t$（Ad-hoc 調整）。

### 2. 本文的研究動機
將死亡計數資料還原為符合精算現實的**離散計數隨機變數 (Count Random Variable)**，透過引進 [[卜瓦松迴歸 (Poisson Regression)]] 框架，建立統計理論完備、一次性極大概似估計 (MLE) 的新李-卡特標準範式。

---

## 二、 核心方法與技術架構 (Methodology & Architecture)

### 1. 卜瓦松對數雙線性模型設定
作者假設在年齡 $x$ 與年份 $t$ 的實際死亡人數 $D_{x,t}$ 服從卜瓦松分佈：
$$D_{x,t} \sim \text{Poisson}(E_{x,t} \mu_{x,t})$$
死亡力 $\mu_{x,t}$ 採用對數雙線性聯結函數 (Log-link function)：
$$\mu_{x,t} = \exp(\alpha_x + \beta_x \kappa_t)$$
即：
$$\ln \mathbb{E}[D_{x,t}] = \ln E_{x,t} + \alpha_x + \beta_x \kappa_t$$
此處 $\ln E_{x,t}$ 作為已知補償項 (Offset)。約束條件維持經典設定：$\sum_t \kappa_t = 0$ 與 $\sum_x \beta_x = 1$。

### 2. 極大概似估計與單維牛頓疊代法 (Goodman 1979 Algorithm)
由於模型中包含非線性雙線性相乘項 $\beta_x \kappa_t$，標準套裝軟體無法直接估計。作者採用 Goodman (1979) 與 Vermunt 的單維牛頓疊代法 (Elementary Newton Method)，逐輪更新參數：

$$\widehat{\theta}^{(\nu+1)} = \widehat{\theta}^{(\nu)} - \frac{\partial L / \partial \theta}{\partial^2 L / \partial \theta^2}$$

對各參數的具體疊代式為：
- **更新 $\alpha_x$**：
  $$\widehat{\alpha}_x^{(\nu+1)} = \widehat{\alpha}_x^{(\nu)} + \frac{\sum_t (D_{x,t} - \widehat{D}_{x,t}^{(\nu)})}{\sum_t \widehat{D}_{x,t}^{(\nu)}}$$
- **更新 $\kappa_t$**：
  $$\widehat{\kappa}_t^{(\nu+1)} = \widehat{\kappa}_t^{(\nu)} + \frac{\sum_x (D_{x,t} - \widehat{D}_{x,t}^{(\nu)}) \widehat{\beta}_x^{(\nu)}}{\sum_x \widehat{D}_{x,t}^{(\nu)} (\widehat{\beta}_x^{(\nu)})^2}$$
- **更新 $\beta_x$**：
  $$\widehat{\beta}_x^{(\nu+1)} = \widehat{\beta}_x^{(\nu)} + \frac{\sum_t (D_{x,t} - \widehat{D}_{x,t}^{(\nu)}) \widehat{\kappa}_t^{(\nu)}}{\sum_t \widehat{D}_{x,t}^{(\nu)} (\widehat{\kappa}_t^{(\nu)})^2}$$
其中 $\widehat{D}_{x,t} = E_{x,t} \exp(\widehat{\alpha}_x + \widehat{\beta}_x \widehat{\kappa}_t)$ 為當前步之預期死亡數。

### 3. 年金反向選擇調整 (Adverse Selection via Brass Relational Model)
除總體人口預測外，作者結合布拉斯關係模型 (Brass Relational Model) 評估壽險年金市場的反向選擇效應：
$$\ln \mu_x^{RA}(t) = \vartheta_1 + \vartheta_2 \ln \mu_x^{NIS}(t)$$
藉此直接量化自願購買年金之被保險人長壽程度對躉繳純保費之加價影響。

---

## 三、 關鍵實驗成果與評測基準 (Empirical Results & Benchmarks)

1. **數據集**：比利時 1960–1998 全國人口死亡資料（年齡 60–98 歲）。
2. **解釋變異數比例**：
   - 在 60–98 歲的大多數年齡層，雙線性時間趨勢解釋了超過 $90\%$ 的時間變異數。
   - **高齡優勢明顯**：在 90 歲以上超高齡層，卜瓦松模型顯著勝過傳統 SVD 方法（整體解釋變異數自 SVD 的 $88.59\%$ 提高至卜瓦松的 $90.79\%$）。
3. **年金現值與反向選擇量化**：
   - 傳統 SVD 傾向高估未來死亡率改善幅度，導致年金現值預測偏高；卜瓦松模型產出相對穩健且適度的死亡改善預測。
   - 年金被保險人因反向選擇效應，其年金純保費需較一般國民生命表調高：**男性增加高達 24%~26%，女性增加 12%~15%**。

---

## 四、 侷限性與批判性反思 (Limitations & Critical Review)

1. **忽略超額離散 (Overdispersion)**：標準卜瓦松假設平均數等於變異數 $\text{Var}(D) = \mathbb{E}[D]$，但在重大流感或氣候異常年份，實際死亡資料常存在明顯的超額離散現象。
2. **仍受制於 Lee-Carter 單因子結構**：模型僅包含一個時間因子 $\kappa_t$，導致跨年齡層的死亡改善完全相關（Trivial Correlation），且未納入世代效應（促成後續 [[2006-renshaw-haberman-cohort]] 的誕生）。

---

## 五、 文獻脈絡與演進關係 (Lineage & Related Work)

- **承接自**：[[李-卡特模型 (Lee-Carter Model)]] (Lee & Carter, 1992)、Alho (2000)、Wilmoth (1993)。
- **被後續廣泛繼承**：成為後續所有隨機死亡率模型（如 Renshaw & Haberman 2006、Plat 2009、O'Hare & Li 2012）的標準最大概似估計框架，亦是 [[2019-levantesi-pizzorusso-ml]] 等機器學習模型對比的 Baseline 基準。
- **跨論文深度對比**：收錄於 [[隨機死亡率模型與機器學習技術演進對比統整]]，探討自經典卜瓦松極大概似估計至現代機器學習之技術演進脈絡。
