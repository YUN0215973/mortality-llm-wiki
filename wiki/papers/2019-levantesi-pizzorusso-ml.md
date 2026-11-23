---
title: 機器學習於死亡率建模與預測之應用：樹模型殘差校正法 (Application of Machine Learning to Mortality Modeling and Forecasting)
aliases: [Levantesi & Pizzorusso 2019, Levantesi 2019, ML Residual Mortality]
authors: [Susanna Levantesi, Virginia Pizzorusso]
year: 2019
institution: [義大利羅馬第一大學統計系 (Sapienza University of Rome), 安永管理顧問 (EY Advisory)]
journal: Risks, 7(1), 26
category: 機器學習死亡率預測 / 樹模型殘差校正 / 整合學習
tags: [machine-learning, decision-trees, random-forests, gradient-boosting, lee-carter, renshaw-haberman, plat-model, residual-correction]
source_pdf: raw/papers/2019_levantesi_pizzorusso_ml.pdf
doi: 10.3390/risks7010026
status: ingested
date: 2026-11-23
---

# 機器學習於死亡率建模與預測之應用：樹模型殘差校正法 (Application of Machine Learning to Mortality Modeling and Forecasting)

> **論文出處**：*Risks*, 7(1), 26. DOI: [10.3390/risks7010026](https://doi.org/10.3390/risks7010026)  
> **作者**：Susanna Levantesi, Virginia Pizzorusso  
> **本機存檔**：`raw/papers/2019_levantesi_pizzorusso_ml.pdf`

---

## 一、 研究背景與核心問題意識 (Motivation & Problem Statement)

### 1. 人口統計學界的「黑盒子 (Black Box)」抗拒心理
儘管機器學習在圖像、金融與非壽險（車險、財產險）領域取得巨大成功，但壽險精算師與人口統計學家長期對機器學習持排斥態度。其主因在於純數據驅動的機器學習缺乏人口統計學的底層理論支撐，決策無法被理性解釋，無法通過保險監管法規對定價與提存準備金的要求。

### 2. 混合型架構的破局思路
如何**既保留傳統隨機死亡率模型的理論可解釋性與結構性先驗，又同時利用機器學習強大的非線性特徵捕捉能力？**
作者提出：**不將機器學習視為傳統模型的「替代品」，而是作為「外掛式殘差校正工具 (Complementary Tool)」**。

---

## 二、 核心方法與技術架構 (Methodology & Architecture)

### 1. 乘法型機器學習估計量 (Multiplicative ML Estimator $\psi_x$)
在卜瓦松死亡計數架構下，實際死亡數為 $D_x \sim \text{Poisson}(\psi_x d_x^{mdl})$，其中 $d_x^{mdl}$ 為特定傳統隨機模型（如 LC, RH, Plat）預期的死亡數。
- 若 $\psi_x \equiv 1$，代表傳統模型完全吻合實際數據。
- 若 $\psi_x \neq 1$，代表傳統模型存在系統性高估或低估。

作者將機器學習演算法應用於**「實際觀察死亡數與傳統模型估計死亡數之比值」**：
$$\frac{D_x}{d_x^{mdl}} \sim \text{gender} + \text{age} + \text{year} + \text{cohort}$$

校正後的死亡率為：
$$m_x^{mdl, ML} = \widehat{\psi}_x^{mdl, ML} \cdot m_x^{mdl}$$

### 2. 評測的三大樹狀演算法
1. **決策樹 (Decision Trees, DT)**：以 `rpart` 套件設定複雜度參數 $cp=0.003$。
2. **[[隨機森林 (Random Forests)]] (RF)**：以 `randomForest` 套件構建 200 棵樹 ($ntree=200$)。
3. **梯度提升 (Gradient Boosting, GB)**：以 `gbm` 套件設定 5000 次迭代、5 折交叉驗證、樹深 $depth=6$、收縮率 $0.001$。

### 3. 李-卡特框架下 ML 估計量的外推預測 (Forecasting Scheme)
傳統機器學習模型本身難以直接進行時間序列外推。作者創造性地將 $\widehat{\psi}_x$ 重新對映回 Lee-Carter 雙線性結構進行預測：
$$\ln(\widehat{\psi}_x^{LC,ML}) = \alpha_a^\psi + \beta_a^{(1,\psi)} \kappa_t^{(1,\psi)}$$
最終形成雙重改善預測式：
$$\ln(m_x^{LC,ML}) = (\alpha_a^\psi + \alpha_a) + \beta_a^{(1,\psi)} \kappa_t^{(1,\psi)} + \beta_a^{(1)} \kappa_t^{(1)}$$
時間參數 $\kappa_t^{(1)}$ 與 $\kappa_t^{(1,\psi)}$ 皆採用帶漂移項隨機漫步外推。

---

## 三、 關鍵實驗成果與評測基準 (Empirical Results & Benchmarks)

1. **數據集**：義大利 1915–2014 全年齡人口死亡率數據（0–100 歲）。
2. **擬合階段 (In-Sample Fit, 1915–2014 MAPE)**：
   - **隨機森林 (RF) 表現最佳**：
     - 李-卡特模型 (LC)：MAPE 自 **$19.48\%$ 暴跌至 $4.85\%$**（改善幅度達 75%）。
     - Renshaw-Haberman (RH)：MAPE 自 **$18.03\%$ 暴跌至 $4.89\%$**。
     - Plat 模型：MAPE 自 **$25.81\%$ 暴跌至 $4.79\%$**（改善幅度達 81%）。
3. **外推預測階段 (Out-of-Sample Forecast, 2000–2014)**：
   - 訓練期 1915–2000，預測 2000–2014：
     - 均方根對數誤差 (RMSLE)：LC-RF 模型在男性上降低了 **$77\%$**，女性降低了 **$71\%$**。
     - 均方根誤差 (RMSE)：LC-RF 模型在女性上改善高達 **$80\%$**。
   - 縮短訓練期 (1960–2000)：改善效果依然顯著，但因歷史樣本減少，高齡段的改善幅度有所收斂。

---

## 四、 侷限性與批判性反思 (Limitations & Critical Review)

1. **對話與質疑：被後續 [[2022-tree-based-mortality]] 批評**：
   - 本文聲稱「RF 殘差能系統性大幅提升預測精確度」，但 Bjerre (2022) 指出：**這項結論高度依賴於「納入了年輕族群 (0–50 歲)」**。若將年齡限制在年金產業關心的 59–89 歲退休人口，純 Lee-Carter 模型在過半數情況下反而優於加裝 RF 的混合模型。
2. **對映回 LC 結構外推的理論矛盾**：將樹模型學到的非線性比值強行壓縮回線性 LC 結構進行 ARIMA 預測，在數學邏輯上存在一定程度的妥協。

---

## 五、 文獻脈絡與演進關係 (Lineage & Related Work)

- **承接自**：[[李-卡特模型 (Lee-Carter Model)]]、[[2006-renshaw-haberman-cohort]]、Plat (2009)、Deprez et al. (2017)。
- **後續引發爭鳴**：開啟了「傳統模型 + 機器學習殘差」的熱潮，直接促成了 Levantesi & Nigri (2019, 2020) 將其延伸至 P-splines 平滑，以及 Bjerre (2022) 針對其局限性的反駁。
- **跨論文深度對比**：收錄於 [[隨機死亡率模型與機器學習技術演進對比統整]]，深入探討殘差混合架構與純樹狀模型之學術爭論。
