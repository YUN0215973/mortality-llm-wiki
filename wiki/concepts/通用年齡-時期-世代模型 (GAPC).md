---
title: 通用年齡-時期-世代模型 (Generalized Age-Period-Cohort Model, GAPC)
aliases: [GAPC, GAPC Model, 通用 APC 模型, 廣義年齡-時期-世代隨機死亡率模型]
category: 精算人口學 / 隨機死亡率模型
tags: [actuarial-science, stochastic-mortality, gapc, glm, lee-carter, cbd]
date: 2026-11-23
---

# 通用年齡-時期-世代模型 (Generalized Age-Period-Cohort Model, GAPC)

> **定義**：通用年齡-時期-世代模型（GAPC）是由 Villegas, Haberman, Kaishev (2014) 與 Hunt & Villegas (2015) 所確立之統一數學理論框架。該架構將過去二十年間精算界發展出的所有主流隨機死亡率模型（包含李-卡特、CBD 家族、Plat 與歐海爾-李模型）統整為具備四大構成要素的廣義非線性回歸體系。

---

## 一、 GAPC 四大核心構成要素

任何屬於 GAPC 體系的隨機死亡率模型，均可嚴格分解為下列四項數學要素：

### 1. 隨機分佈要素 (Random Component)
假設特定年齡 $x$ 與年份 $t$ 的實際死亡計數 $D_{x,t}$ 服從指數族分佈（Exponential Family），最常見兩種精算設定：
- **卜瓦松分佈 (Poisson)**：$D_{x,t} \sim \text{Poisson}(E_{x,t} \mu_{x,t})$，適用於死亡力（Force of Mortality）連續建模。
- **二項分佈 (Binomial)**：$D_{x,t} \sim \text{Binomial}(L_{x,t}, q_{x,t})$，適用於初存人數（Initial Exposures）與死亡機率離散建模。

### 2. 系統性預測元 (Systematic Component)
死亡率對數或勝算比的預測結構 $\eta_{x,t}$ 採用年齡、時期與世代因子的廣義相加/雙線性組合：
$$\eta_{x,t} = \alpha_x + \sum_{i=1}^N \beta_x^{(i)} \kappa_t^{(i)} + \beta_x^{(0)} \gamma_{t-x}$$
其中：
- $\alpha_x$：基礎年齡輪廓（Baseline Age Profile）。
- $\kappa_t^{(i)}$：第 $i$ 個隨時期 $t$ 變化的巨觀趨勢因子。
- $\beta_x^{(i)}$：年齡 $x$ 對第 $i$ 個時期因子的敏感度權重（可為固定函數或自由待估參數）。
- $\gamma_{t-x}$：出生世代因子（Cohort Effect，出生年 $c = t - x$）。
- $\beta_x^{(0)}$：不同年齡對世代效應的調節因子（通常設為 $1$）。

### 3. 聯結函數 (Link Function)
將預測元 $\eta_{x,t}$ 對映至死亡統計量：
- **對數聯結 (Log Link)**：$\ln \mu_{x,t} = \eta_{x,t}$（李-卡特、RH、Plat、O'Hare-Li 採用）。
- **對數勝算聯結 (Logit Link)**：$\text{logit}\, q_{x,t} = \ln \left( \frac{q_{x,t}}{1 - q_{x,t}} \right) = \eta_{x,t}$（CBD 家族 M5–M8 採用）。

### 4. 參數唯一識別約束 (Identifiability Constraints)
由於模型中存在多重雙線性相乘項（$\beta_x^{(i)} \kappa_t^{(i)}$）以及年齡、時期、世代的線性重疊（$c = t - x$），必須引入一組嚴格的數學等式約束，以保證極大概似估計（MLE）解的唯一性（如 $\sum_x \beta_x^{(i)} = 1$、$\sum_t \kappa_t^{(i)} = 0$、$\sum_c \gamma_c = 0$、$\sum_c c \gamma_c = 0$）。

---

## 二、 主流隨機死亡率模型在 GAPC 體系之映射表

| 模型代號 | 原始文獻 | 聯結函數 | 預測元結構 $\eta_{x,t}$ | 核心特色與適用年齡段 |
| :--- | :--- | :--- | :--- | :--- |
| **M1** | [[李-卡特模型 (Lee-Carter Model)]] (1992, [[2002-brouhns-poisson-lc]]) | $\ln \mu_{x,t}$ | $\alpha_x + \beta_x \kappa_t$ | 單一時間因子，無世代效應，全年齡 |
| **M2** | [[2006-renshaw-haberman-cohort]] | $\ln \mu_{x,t}$ | $\alpha_x + \beta_x^{(1)} \kappa_t + \beta_x^{(0)} \gamma_{t-x}$ | 引入世代效應，但容易不收斂 |
| **M3** | Currie APC (2006) | $\ln \mu_{x,t}$ | $\alpha_x + \kappa_t + \gamma_{t-x}$ | $\beta_x$ 固定為 1，結構簡約 |
| **M5** | [[2006-cairns-two-factor-cbd]] | $\text{logit}\, q_{x,t}$ | $\kappa_t^{(1)} + \kappa_t^{(2)}(x - \bar{x})$ | 二因子（截距+斜率），專注高齡 (60+) |
| **M6** | Cairns et al. (2009) | $\text{logit}\, q_{x,t}$ | $\kappa_t^{(1)} + \kappa_t^{(2)}(x - \bar{x}) + \gamma_{t-x}$ | CBD 加入世代效應 |
| **M7** | [[2007-cairns-comparison-stochastic]] | $\text{logit}\, q_{x,t}$ | $\kappa_t^{(1)} + \kappa_t^{(2)}(x - \bar{x}) + \kappa_t^{(3)}\left((x - \bar{x})^2 - \sigma_x^2\right) + \gamma_{t-x}$ | CBD 加入二次年齡項與世代因子，穩健性最高 |
| **M8** | Cairns et al. (2009) | $\text{logit}\, q_{x,t}$ | $\kappa_t^{(1)} + \kappa_t^{(2)}(x - \bar{x}) + \gamma_{t-x}^{(1)} + \gamma_{t-x}^{(2)}(x_c - x)$ | 考慮世代效應隨年齡高齡衰減 |
| **M9** | [[2009-plat-stochastic-mortality|Plat (2009)]] | $\ln \mu_{x,t}$ | $\alpha_x + \kappa_t^{(1)} + \kappa_t^{(2)}(\bar{x} - x) + \kappa_t^{(3)}(\bar{x} - x)^+ + \gamma_{t-x}$ | 結合 LC 與 CBD，三時期因子+世代，全年齡 |
| **M10** | [[2012-ohare-li-young-mortality]] | $\ln \mu_{x,t}$ | $\alpha_x + \kappa_t^{(1)} + \kappa_t^{(2)}(\bar{x} - x) + \kappa_t^{(3)}\left((\bar{x} - x)^2 - \sigma_x^2\right) + \gamma_{t-x}$ | Plat 改良版，以二次項取代折線項，擬合幼年與意外凸起 |

---

## 三、 GAPC 框架的估計與預測工作流程

1. **參數擬合 (Calibration)**：
   - 使用牛頓-拉弗森演算法 (Newton-Raphson) 或費雪計分法 (Fisher Scoring) 進行交替單變量搜尋（Iterative Coordinate Descent），極大化卜瓦松或二項對數概似函數。
2. **時間序列動態建模 (Dynamic Extrapolation)**：
   - 時期因子 $\boldsymbol{\kappa}_t = (\kappa_t^{(1)}, \dots, \kappa_t^{(N)})^T$ 擬合多變量隨機游走漂移過程 (Multivariate Random Walk with Drift, MRWD)：
     $$\boldsymbol{\kappa}_t = \boldsymbol{\mu} + \boldsymbol{\kappa}_{t-1} + \boldsymbol{Z}_t, \quad \boldsymbol{Z}_t \sim \mathcal{N}(\mathbf{0}, \boldsymbol{\Sigma})$$
   - 世代因子 $\gamma_c$ 通常獨立擬合單變量 $\text{ARIMA}(p,d,q)$ 過程。
3. **蒙地卡羅情境生成 (Scenario Simulation)**：
   - 藉由採樣 $\boldsymbol{Z}_t$ 模擬未來數十年的死亡率路徑，生成預測信賴區間與扇形圖（Fan Charts），為年金與長壽衍生品定價。

---

## 四、 GAPC 框架之侷限與現代機器學習的超越

儘管 GAPC 體系奠定了精算統計學的堅實基礎，但在面對巨量數據與複雜人口特徵時暴露了內生缺陷：
1. **加法與雙線性假設之剛性**：
   - GAPC 限制年齡、時期與世代以預設的相加或單純相乘形式呈現，無法捕捉如「特定世代在特定年代遭遇經濟危機所引發之非線性年齡死亡激增」。
2. **數值收斂與維度災難**：
   - 當擴展至多因子與世代項時（如 M2），參數空間急遽擴張且極概似曲面呈現高度多峰性，收斂失敗率偏高。
3. **機器學習範式的突破**：
   - [[隨機森林 (Random Forests)]] 與 [[隨機梯度提升 (Stochastic Gradient Boosting)]]（[[2022-tree-based-mortality]]）透過非參數樹狀分裂，打破了線性/雙線性結構束縛；
   - 深度學習（[[2018-hainaut-neural-analyzer]]、[[2019-nigri-deep-learning-lc]]）利用神經網絡自編碼降維與 LSTM 記憶單元，徹底解放了對固定基底函數與嚴格平穩性假設的依賴。

---

## 五、 相關文獻與交叉引用

- [[2002-brouhns-poisson-lc]]：奠定 GAPC 框架中卜瓦松極大概似估計之開山之作。
- [[2006-cairns-two-factor-cbd]]：開創二項對數勝算比架構 (M5)。
- [[2006-renshaw-haberman-cohort]]：GAPC 架構下最經典的世代擴充模型 (M2)。
- [[2007-cairns-comparison-stochastic]]：GAPC 體系內部 M1–M8 之大型實證對比評測。
- [[2009-plat-stochastic-mortality]]：融匯 LC 與 CBD 兩大學派之全年齡經典 M9 模型。
- [[2012-ohare-li-young-mortality]]：將 GAPC 體系推向全年齡段的最優結構 (M10)。
- [[2017-deprez-ml-mortality-modeling]]：首度以機器學習決策樹與梯度提升檢驗 GAPC 體系之結構殘差。
- [[2022-tree-based-mortality]]：評估樹狀機器學習模型相較於 GAPC 體系九大模型的優勢與邊界。
- [[李-卡特模型 (Lee-Carter Model)]]：GAPC 體系之核心始祖。
- [[世代效應 (Cohort Effect)]]：GAPC 體系處理的核心動態現象之一。
- [[長壽風險 (Longevity Risk)]]：GAPC 體系應用之最核心金融風險領域。
