---
title: 隨機梯度提升 (Stochastic Gradient Boosting)
aliases: [Gradient Boosting, GBM, Stochastic Gradient Boosting]
tags: [machine-learning, ensemble-learning, boosting, decision-trees]
status: active
date: 2026-11-23
---

# 隨機梯度提升 (Stochastic Gradient Boosting)

## 一、 核心概念與理論機制

**隨機梯度提升 (Stochastic Gradient Boosting)** 是由 Jerome H. Friedman 於 2001 與 2002 年提出之代表性 Boosting 演算法。

相較於隨機森林的平行獨立構樹，梯度提升採用**序列漸進迭代 (Sequential Optimization)** 機制：每一輪迭代新生成的決策樹（弱學習器）均用來擬合上一輪全體模型的負梯度向量（即殘差近似值）：

$$\widehat{m}_k(\mathcal{F}) = \widehat{m}_{k-1}(\mathcal{F}) + \nu \sum_{j=1}^{J_k} \gamma_{j,k} I(\mathcal{F} \in R_{j,k})$$

其中：
- $\nu \in (0, 1]$：學習率或收縮率 (Shrinkage Rate)，控制每一步更新的步長，較小的步長能顯著抑制過擬合。
- $R_{j,k}$：第 $k$ 棵樹的終端葉節點區域。
- $\gamma_{j,k}$：該節點對應的最佳輸出權重。

### 隨機化擴展 (Stochastic Subsampling)
Friedman (2002) 證明，在每一輪迭代中僅隨機抽取子樣本（如 `bag.fraction = 0.5`）進行樹的擬合，不僅大幅加快計算速度，更能引入噪音破除局部極值，提升泛化表現。

---

## 二、 在死亡率長程預測中的表現

在 [[2022-tree-based-mortality]] 跨 33 國之大尺度評測中：
- 梯度提升模型配置為：$n.trees=6000$、樹深 $depth=4$、學習率 $\nu=0.001$、隨機抽樣比例 $0.5$。
- **實證優勢**：在 30 年超長期預測且針對高齡退休人口 (59–89 歲) 的情境下，**純梯度提升模型 (Pure GB)** 在 [[模式信賴集合 (Model Confidence Set, MCS)]] 評定下進入優勢模型集合的頻率高達 **$53\%$** 與 **$45\%$**，名列全體 31 種模型之冠。
