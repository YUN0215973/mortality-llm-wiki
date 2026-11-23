---
title: 卷積神經網絡於死亡率預測 (Convolutional Neural Networks for Mortality, CNN)
aliases: [CNN Mortality Forecasting, 卷積神經網路死亡率曲面建模]
category: 人工智慧與深度學習 / 死亡率建模 / 影像網格特徵提取
tags: [deep-learning, cnn, mortality-forecasting, convolutional-neural-networks, spatial-temporal, bootstrap, solvency-ii]
date: 2026-11-23
---

# 卷積神經網絡於死亡率預測 (Convolutional Neural Networks for Mortality, CNN)

> **定義**：在現代精算科學與深度學習死亡率預測中，卷積神經網絡（CNN）代表了一種跳脫傳統「一維時間序列」的全新建模視角。該方法將年齡-時期的歷史對數死亡率曲面重構為類似數位影像的「二維時空網格矩陣（2D Spatial-Temporal Grid）」，透過滑動卷積核（Convolutional Kernels）同時擷取相鄰年齡、年份趨勢以及沿對角線分佈的「出生世代效應（Cohort Effect）」。

---

## 一、 技術設計直覺：將死亡率曲面視為二維影像

傳統精算模型（如 Lee-Carter）將各年齡視為獨立通道，或依賴固定的相加結構。CNN 則借鑒了計算機視覺處理圖像特徵的局部感受野（Receptive Field）機制：

1. **張量表述**：
   輸入矩陣 $\mathbf{M} \in \mathbb{R}^{X \times T}$，其中橫軸為歷史年份 $t \in [1, T]$，縱軸為連續年齡 $x \in [1, X]$，矩陣元素為對數死亡率 $\ln m_{x,t}$。
2. **多維度特徵卷積核 (Convolutional Filters)**：
   卷積核在矩陣上滑動計算特徵圖（Feature Maps）：
   $$h_{i,j}^{(k)} = \text{ReLU}\left( \sum_{u=0}^{K_x-1} \sum_{v=0}^{K_t-1} W_{u,v}^{(k)} \cdot M_{i+u, j+v} + b^{(k)} \right)$$
   - **橫向卷積**：捕捉特定年齡隨時間變化的長期改善斜率（時期效應）；
   - **縱向卷積**：捕捉相鄰年齡之間的死亡連續性與平滑性（年齡效應）；
   - **對角線感受野**：由於 $t - x = c$ 為出生年份恆等式，二維卷積核能**自然跨越對角線單元，無須人為指定約束條件即可自動提取世代效應**。

---

## 二、 破解不確定性瓶頸：拔靴重抽法 (Bootstrapping for CNN)

針對精算學界對深度學習「只能產出點預測、缺乏預測區間」的質疑，[[2021-schnurch-korn-neural-networks|Schnürch & Korn (2021)]] 提出了結合殘差拔靴法（Residual Bootstrap）的完整解決方案：
1. 訓練 CNN 得到配適曲面，計算標準化經驗殘差池。
2. 進行 $B = 1,000$ 次殘差有放回抽樣，生成千組歷史合成路徑並重新校正網絡。
3. 外推未來的經驗分佈，產出 90%、95% 與 99.5% 的預測區間（Prediction Intervals）。
4. **監理合規意義**：使深度學習模型首度具備產出符合歐盟 Solvency II 與台灣 ICS 資本要求之能力。

---

## 三、 與傳統模型及其他深度學習架構之橫向對比

| 特徵維度 | 李-卡特模型 (Lee-Carter) | 循環神經網絡 ([[長短期記憶網路 (Long Short-Term Memory, LSTM)\|LSTM]]) | 卷積神經網絡 (CNN) | 純樹狀模型 ([[隨機梯度提升 (Stochastic Gradient Boosting)\|GB/RF]]) |
| :--- | :--- | :--- | :--- | :--- |
| **數據表徵視角** | 一維空間降維 + 時間序列 | 一維序列記憶 | 二維空間-時間影像矩陣 | 表格型特徵矩陣 (Tabular) |
| **世代效應捕捉** | 無法直接捕捉 (需加 M2) | 需額外輸入特徵 | 卷積核對角線自動提取 | 需透過特徵工程或一階差分 |
| **點預測精度** | 基準 (較低) | 極高 (降低40%~91%) | 極高 (與 LSTM 相當) | 極高 (長跨度勝率最高) |
| **區間預測能力** | 解析閉式解 (最簡便) | 需複雜重抽樣 | 拔靴法實證吻合度高 | 需重抽樣或分位數迴歸 |
| **計算算力開銷** | 極低 (秒級) | 中等 (GPU 訓練) | 較高 (拔靴需上千次訓練) | 低至中等 (CPU 平行運算) |

---

## 四、 相關文獻與交叉引用

- [[2021-schnurch-korn-neural-networks]]：首度提出 CNN 死亡率預測與拔靴區間估計的開創之作。
- [[2018-hainaut-neural-analyzer]]：利用自編碼器進行非線性降維的前行研究。
- [[2019-nigri-deep-learning-lc]]：利用 LSTM 進行時期維度外推的序列對標模型。
- [[2024-qiao-wang-ml-long-term-mortality]]：借鑒影像鄰域空間概念進一步發展樹集成模型之最新成果。
- [[長壽風險 (Longevity Risk)]]：CNN 區間預測服務的最核心精算業務目標。
