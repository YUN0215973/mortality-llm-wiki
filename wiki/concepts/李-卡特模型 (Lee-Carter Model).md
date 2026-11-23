---
title: 李-卡特模型 (Lee-Carter Model)
aliases: [Lee-Carter, LC Model]
tags: [actuarial-science, demography, mortality, stochastic-models]
status: active
date: 2026-11-23
---

# 李-卡特模型 (Lee-Carter Model)

## 一、 概念定義與歷史地位

**李-卡特模型 (Lee-Carter Model, LC)** 是由 Ronald D. Lee 與 Lawrence R. Carter 於 1992 年在《*Journal of the American Statistical Association*》提出的經典隨機死亡率模型。

作為現代隨機人口預測學的奠基之作，它徹底取代了過去僅依賴主觀專家推估的靜態生命表方法，並演化成為今日 [[通用年齡-時期-世代模型 (GAPC)]] 系列的共同始祖。

---

## 二、 數學形式與參數量化

李-卡特模型將年齡 $x$ 於時期 $t$ 之中心死亡率 $m_{x,t}$ 之自然對數分解為靜態年齡效應與時間變動效應的線性組合：

$$\ln(m_{x,t}) = \alpha_x + \beta_x \kappa_t + \epsilon_{x,t}$$

其中：
- $\alpha_x$：**基準年齡輪廓 (Static Age Profile)**，代表各年齡層在整個歷史期間的平均對數死亡水準。
- $\kappa_t$：**時期死亡率指數 (Time Index)**，代表隨時間變化的全體死亡率總體水準（通常呈現遞減走勢）。
- $\beta_x$：**年齡敏感度係數 (Age-Response Modulation)**，描述特定年齡 $x$ 對總體時間趨勢 $\kappa_t$ 變化的敏感程度。
- $\epsilon_{x,t}$：平均值為 0、變異數為常數的隨機殘差項。

**模型辨識度約束條件 (Identifiability Constraints)**：
為確保參數估計的唯一性，通常施加標準規範：
$$\sum_t \kappa_t = 0, \quad \sum_x \beta_x = 1$$
預測時，先透過奇異值分解 (SVD) 或卜瓦松最大概似估計 (Poisson MLE) 校正參數，再使用 Box-Jenkins 時間序列分析法對 $\kappa_t$ 擬合帶有漂移項之隨機漫步模型 (Random Walk with Drift, RWD)：
$$\kappa_t = \kappa_{t-1} + d + e_t$$

---

## 三、 模型侷限性與後續演進脈絡

儘管李-卡特模型具有形式簡潔、易於解釋的優點，但其在長壽風險評估中面臨多項實證瓶頸：
1. **單一因子假設過於嚴苛**：無法捕捉「年齡-時期」的交互作用與非平行移動。
2. **缺乏世代效應 (Cohort Effect)**：促成 Renshaw & Haberman (2006) 提出加入世代項的 RH 模型。
3. **無法應對「死亡率改善旋轉」**：Li et al. (2013) 發現年輕族群改善減緩、高齡族群改善加速，原始 LC 模型難以因應。
4. **機器學習的挑戰**：
   - 在 [[2022-tree-based-mortality]] 中，實證結果證明傳統 LC 模型及其殘差混合模型在 30 年長期預測下，顯著落後於去除先驗限制的 [[隨機梯度提升 (Stochastic Gradient Boosting)]] 與 [[隨機森林 (Random Forests)]]。
