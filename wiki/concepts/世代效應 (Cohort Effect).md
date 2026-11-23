---
title: 世代效應 (Cohort Effect)
aliases: [Cohort Effect, 出生年效應, 出生世代效應]
category: 精算人口學 / 隨機死亡率模型
tags: [actuarial-science, demography, cohort-effect, stochastic-mortality, gapc]
date: 2026-11-23
---

# 世代效應 (Cohort Effect)

> **定義**：在人口學與精算科學中，「世代效應」指特定出生年份（$c = t - x$，其中 $t$ 為曆年、$x$ 為年齡）的人口群體在其生命歷程中所表現出與其他世代系統性相異的死亡率改善特徵。

---

## 一、 人口學背景與經典現象：「黃金世代」

世代效應源自特定歷史背景下環境、衛生、飲食與生活型態的長期印記：
1. **英國黃金世代 (The UK Golden Cohort)**：
   - Willets (2004) 與精算界觀察到，出生於 1925 年至 1945 年之間（特別是 1931 年前後）的英國人口，在整個人生階段都呈現出顯著高於前後世代的死亡率改善速度。
   - **成因**：童年經歷二戰配給制（低脂肪均衡飲食）、青少年期抗生素普及與英國國民保健署 (NHS) 成立、壯年期男性吸菸率劇降等綜合因素。
2. **對年金與長壽風險的衝擊**：
   - 若模型忽視世代效應，將嚴重**低估**高齡年金領取者的平均餘命，導致保險公司與退休基金產生巨額長壽風險準備金不足。

---

## 二、 隨機死亡率模型中的數學表述

在 [[通用年齡-時期-世代模型 (GAPC)]] 框架下，世代參數通常以 $\gamma_{t-x}$（或 $\gamma_c$）表示：

### 1. 倫蕭-哈伯曼模型 (Renshaw-Haberman, 2006 / M2)
作為 [[李-卡特模型 (Lee-Carter Model)]] 的世代擴展：
$$\ln m_{x,t} = \alpha_x + \beta_x^{(1)} \kappa_t + \beta_x^{(0)} \gamma_{t-x}$$
- 其中 $\beta_x^{(0)}$ 衡量不同年齡對世代效應的敏感度。
- **限制**：此結構具高度非線性與多峰對數概似函數，存在嚴重的參數辨識困難與數值演算法不收斂問題。

### 2. 凱恩斯-布雷克-道德模型家族 (CBD Extensions / M6, M7, M8)
Cairns et al. (2009) 在標準 CBD (M5) 基礎上擴充世代因子：
- **M6 (CBD with Cohort)**：
  $$\text{logit}\, q_{x,t} = \kappa_t^{(1)} + \kappa_t^{(2)} (x - \bar{x}) + \gamma_{t-x}$$
- **M7 (CBD Quadratic with Cohort)**：
  $$\text{logit}\, q_{x,t} = \kappa_t^{(1)} + \kappa_t^{(2)} (x - \bar{x}) + \kappa_t^{(3)} \left((x - \bar{x})^2 - \sigma_x^2\right) + \gamma_{t-x}$$
- **M8 (CBD with Age-Modulated Cohort)**：
  $$\text{logit}\, q_{x,t} = \kappa_t^{(1)} + \kappa_t^{(2)} (x - \bar{x}) + \gamma_{t-x}^{(1)} + \gamma_{t-x}^{(2)} (x_c - x)$$
  引入高齡衰減因子，假設世代效應隨年紀增長逐漸收斂。

### 3. 歐海爾-李模型 (O'Hare & Li, 2012 / M10)
將 Plat (2009) 與 M7 架構整合，使世代效應適用於全年齡段（0–89 歲）：
$$\ln m_{x,t} = \alpha_x + \kappa_t^{(1)} + \kappa_t^{(2)} (\bar{x} - x) + \kappa_t^{(3)} \left((\bar{x} - x)^2 - \sigma_x^2\right) + \gamma_{t-x}$$

---

## 三、 參數辨識與預測挑戰 (Identification & Projection Issues)

1. **內生共線性問題 (Intrinsic Colinearity)**：
   - 由於數學恆等式 $c = t - x$，模型中的時期效應與年齡、世代產生線性重疊。
   - 必須施加額外線性約束條件（如 $\sum_c \gamma_c = 0$ 且 $\sum_c c \gamma_c = 0$）以確保參數唯一可辨識。
2. **新世代預測的外推 (Cohort Extrapolation)**：
   - 在預測期 $T+1, T+2, \dots$ 時，未來的世代尚未有充足歷史觀測值。
   - 通常採用單變量 ARIMA 過程（如 $\text{ARIMA}(1,1,0)$ 或隨機游走漂移項）對 $\gamma_c$ 進行獨立外推，容易擴大預測的不確定性信賴區間。

---

## 四、 機器學習視角下的世代特徵處理

在現代機器學習死亡率模型中，處理世代效應具備不同技術途徑：
- **特徵工程法**：直接將出生年 $c = t - x$ 與年齡 $x$、年份 $t$ 並列為樹狀模型輸入特徵（[[隨機森林 (Random Forests)]]、[[隨機梯度提升 (Stochastic Gradient Boosting)]]）。如 [[2022-tree-based-mortality]] 所示，純樹模型透過多重決策分裂能自然捕捉非線性的世代互動，但對未來全新世代的外推能力需謹慎驗證。
- **殘差混合法**：在第一階段先由含世代效應的傳統模型（如 M2 或 M7）濾除宏觀世代趨勢，第二階段再以機器學習（[[2019-levantesi-pizzorusso-ml]]）擬合年齡與時期殘差。

---

## 五、 相關文獻與交叉引用

- [[2006-renshaw-haberman-cohort]]：首度為李-卡特模型正式引入世代效應 ($\text{LC}+\text{Cohort}$ / M2)。
- [[2007-cairns-comparison-stochastic]]：全面對比 M1–M8，確立 M7 (含二次年齡項與世代因子) 的穩健性優勢。
- [[2012-ohare-li-young-mortality]]：將世代效應建模成功延伸至全年齡段 (M10)。
- [[2022-tree-based-mortality]]：探討樹狀模型如何透過差分與特徵互動替代傳統世代參數。
- [[李-卡特模型 (Lee-Carter Model)]]：未考慮世代效應之基準模型。
- [[通用年齡-時期-世代模型 (GAPC)]]：世代效應之一般化統一理論框架。
