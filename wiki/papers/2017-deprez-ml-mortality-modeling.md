---
title: 機器學習技術於死亡率建模之應用 (Machine learning techniques for mortality modeling)
aliases: [Deprez 2017, ML for Mortality, 開山之作]
authors: [Philippe Deprez, Pavel V. Shevchenko, Mario V. Wüthrich]
year: 2017
institution: [瑞士蘇黎世聯邦理工學院 (ETH Zurich), 澳洲麥覺理大學 (Macquarie University)]
journal: European Actuarial Journal, 7(2), 337–352
category: 機器學習 / 死亡率建模 / 梯度提升決策樹 / 死因別死亡率
tags: [actuarial-science, machine-learning, gradient-boosting, decision-trees, lee-carter, cause-of-death, model-validation]
source_pdf: raw/papers/2017_deprez_ml_mortality_modeling.pdf
doi: 10.1007/s13385-017-0152-4
status: ingested
date: 2026-11-23
---

# 機器學習技術於死亡率建模之應用 (Machine learning techniques for mortality modeling)

> **論文出處**：*European Actuarial Journal*, 7(2), 337–352 (2017). DOI: [10.1007/s13385-017-0152-4](https://doi.org/10.1007/s13385-017-0152-4)  
> **作者**：Philippe Deprez, Pavel V. Shevchenko, Mario V. Wüthrich (精算學界機器學習先驅)  
> **本機存檔**：`raw/papers/2017_deprez_ml_mortality_modeling.pdf`

---

## 一、 研究背景與核心問題意識 (Motivation & Problem Statement)

### 1. 傳統精算模型的結構性盲區
自 1992 年李-卡特模型問世以來的二十餘年間，精算學界始終受困於參數模型與廣義非線性模型（GNM）的預設數學形式：
- 若模型擬合殘差存在系統性自相關，精算師往往只能透過人工試誤法（Trial-and-Error）不斷疊加二階項或世代因子；
- 傳統模型極難處理**高維特徵與死因別死亡率（Cause-of-Death, CoD）**的交互作用。

### 2. 本文的歷史性開創地位
本文是**國際精算學術界第一篇將現代機器學習演算法（特別是迴歸樹與隨機梯度提升）正式導入死亡率建模與模型驗證的奠基之作**。作者旨在展示：
- 機器學習如何作為強大的診斷工具，自動檢測傳統模型（如 Lee-Carter）的結構性缺失；
- 機器學習如何打破參數假設限制，直接對不同死因（癌症、心血管疾病等）的死亡率曲面進行高維非線性擬合。

---

## 二、 核心方法與技術架構 (Methodology & Architecture)

### 1. 迴歸決策樹與梯度樹提升 (Regression Trees & Gradient Boosting)
- **迴歸樹 (CART)**：將年齡 $x$ 與時期 $t$ 的特徵空間劃分為非重疊的矩形區域 $R_m$，每個區域預測為一常數值 $c_m$：
  $$f(x,t) = \sum_{m=1}^M c_m \cdot \mathbb{I}\{(x,t) \in R_m\}$$
- **梯度樹提升 (Gradient Boosting)**：以加法式模型序列迭代弱學習器：
  $$F_K(x,t) = F_0(x,t) + \sum_{k=1}^K \nu \cdot h_k(x,t)$$
  其中 $\nu \in (0,1]$ 為學習率（Shrinkage parameter），每一步以擬合負梯度（Pseudo-residuals）為目標。

### 2. 兩大核心應用範式

#### 範式 A：模型檢驗與殘差結構自動萃取 (Model Validation via ML)
設傳統模型（如 [[李-卡特模型 (Lee-Carter Model)]]）估計出的死亡力為 $\widehat{\mu}_{x,t}^{\text{LC}}$，定義觀測殘差：
$$r_{x,t} = \ln \left( \frac{D_{x,t}}{E_{x,t}} \right) - \ln \widehat{\mu}_{x,t}^{\text{LC}}$$
利用梯度提升樹擬合殘差函數 $g(x,t)$。
- **診斷判據**：若提升樹無法從殘差中學習到有效特徵（即預測值收斂於 0），代表傳統模型結構已充分捕捉信息；反之，若提升樹能顯著分裂出非零節點，則直接精確指出了李-卡特模型的結構性缺陷區域。

#### 範式 B：死因別死亡率非線性建模 (Cause-of-Death Modeling)
針對五大死因（腫瘤、循環系統疾病、呼吸系統疾病、外部死因、其他）同時建模，容納各死因在不同年齡段的異質性改善速度。

---

## 三、 關鍵實驗成果與評測基準 (Empirical Results & Benchmarks)

1. **實證數據**：瑞士 (Switzerland) 歷史人口與五大死因登記數據（1970–2014，年齡 20–89 歲）。
2. **李-卡特模型的結構性缺陷診斷**：
   - 梯度提升樹在殘差擬合中迅速鎖定了多個顯著分裂點，清晰揭示：李-卡特模型在瑞士男性 60–75 歲區間系統性低估了死亡率改善幅度，並自動捕捉到了未被納入的弱世代效應。
3. **死因別死亡率擬合**：
   - 樹狀模型展現了卓越的高維彈性，能精準捕捉心血管疾病在老年期的崩跌式改善與青年男性外部死因（意外事故）的獨立凸起特徵。

---

## 四、 侷限性與批判性反思 (Limitations & Critical Review)

1. **僅限於樣本內驗證與短期配適，未處理長程時間序列外推**：
   - 本文側重於模型診斷與擬合能力展示，並未提出決策樹如何跨越 20–30 年進行未見年份的時間外推（該問題隨後由 [[2022-tree-based-mortality]] 透過一階差分轉換正式突破）。
2. **缺乏精算封閉式信賴區間**：
   - 樹模型無法像廣義線性模型一樣直接輸出漸近變異數矩陣。

---

## 五、 文獻脈絡與演進關係 (Lineage & Related Work)

- **承接自**：Breiman et al. (1984) CART、Friedman (2001) 梯度提升、[[李-卡特模型 (Lee-Carter Model)]]。
- **歷史性啟發與深遠影響**：
  - **本文為整個精算領域開啟了「機器學習死亡率研究」的大門**！
  - 直接啟發了 [[2019-levantesi-pizzorusso-ml]] 將樹模型殘差混合正式發展為二階段預測模型；
  - 亦促成了 [[2020-levantesi-longevity-ml]] 的長壽風險綜述與 [[2022-tree-based-mortality]] 差分純樹模型的橫空出世。
- **跨論文深度對比**：收錄於 [[隨機死亡率模型與機器學習技術演進對比統整]]。
