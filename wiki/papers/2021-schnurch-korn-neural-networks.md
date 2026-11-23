---
title: 基於神經網絡之死亡率點預測與區間預測 (Point and interval forecasts of death rates using neural networks)
aliases: [Schnürch & Korn 2021, CNN 死亡率預測, ASTIN 2022]
authors: [Simon Schnürch, Ralf Korn]
year: 2021
institution: [德國凱撒斯勞滕工業大學 (TU Kaiserslautern), 德國弗勞恩霍夫工業數學研究所 (Fraunhofer ITWM)]
journal: ASTIN Bulletin: The Journal of the IAA, 52(2), 333–360 (2022)
category: 深度學習 / 卷積神經網絡 (CNN) / 拔靴法不確定性量化 / Solvency II
tags: [actuarial-science, deep-learning, convolutional-neural-networks, cnn, interval-forecasting, bootstrap, uncertainty-quantification, lee-carter]
source_pdf: raw/papers/2021_schnurch_korn_neural_networks.pdf
doi: 10.1017/asb.2021.32
status: ingested
date: 2026-11-23
---

# 基於神經網絡之死亡率點預測與區間預測 (Point and interval forecasts of death rates using neural networks)

> **論文出處**：*ASTIN Bulletin: The Journal of the IAA*, 52(2), 333–360 (2022 / 線上發表 2021). DOI: [10.1017/asb.2021.32](https://doi.org/10.1017/asb.2021.32)  
> **作者**：Simon Schnürch, Ralf Korn  
> **本機存檔**：`raw/papers/2021_schnurch_korn_neural_networks.pdf`

---

## 一、 研究背景與核心問題意識 (Motivation & Problem Statement)

### 1. 深度學習在精算實務上的「阿基里斯之腱」
自 2018 年以來，精算學界相繼引進多層感知機 (MLP)、自編碼器 (Autoencoders) 與循環神經網路 ([[2019-nigri-deep-learning-lc|LSTM]])，並在死亡率的點預測指標（RMSE、MAPE）上大幅超越了傳統的李-卡特模型。然而，如 [[2020-levantesi-longevity-ml|Levantesi et al. (2020)]] 綜述所嚴厲指出的：
> **神經網絡本質上只能產出單一數值的「點預測 (Point Forecast)」，完全無法像 ARIMA 導出「預測區間 (Prediction Intervals)」與不確定性分佈！**

### 2. 歐盟 Solvency II 與保險監理的強制合規要求
保險公司提存長壽風險償付能力資本（SCR）與發行年金商品時，監理機關要求評估的是 99.5% 1年 VaR 或完整的尾端隨機情境（Fan Charts）。**若無法提供嚴謹的預測區間，任何預測精度再高的深度學習模型都無法被核准為法定精算內模**。

### 3. 本文的核心使命
設計一套**基於卷積神經網絡 (Convolutional Neural Networks, CNN) 的架構**，並開創性地結合**拔靴重抽樣法 (Bootstrapping)**，徹底攻克深度學習在死亡率區間預測與不確定性量化上的理論瓶頸。

---

## 二、 核心方法與技術架構 (Methodology & Architecture)

### 1. 二維影像視角的卷積神經網路 (CNN for Mortality Surfaces)
不同於 LSTM 將死亡率視為一維時間序列，本文將年齡-時期對數死亡率矩陣視為 **2D 網格影像 (2D Spatial-Temporal Grid)**：
- **輸入張量**：$\mathbf{X} \in \mathbb{R}^{A \times T}$，其中橫軸為年份，縱軸為年齡。
- **2D 卷積核 (Convolutional Kernels)**：
  滑動濾波器（Filter）同時在年齡與時間兩個維度提取局部特徵：
  $$h_{i,j} = \sigma\left( \sum_{u} \sum_{v} w_{u,v} x_{i+u, j+v} + b \right)$$
  - 橫向滑動：捕捉跨年份的技術進步與醫療改善（時期效應）；
  - 縱向滑動：捕捉相鄰年齡層的連續性（年齡效應）；
  - **對角線滑動**：卷積自然涵蓋對角線方向（$t - x = c$），**無須人工額外定義即可自動提取出生世代效應 (Cohort Effect)**！

### 2. 神經網絡拔靴重抽樣法 (Neural Network Bootstrapping)
為了量化預測不確定性，作者提出專門針對深度學習的殘差重抽架構：
1. **模型配適**：以歷史數據訓練 CNN 得到配適死亡率 $\widehat{m}_{x,t}$，計算標準化殘差 $\epsilon_{x,t}$。
2. **殘差重抽**：自經驗殘差池中進行有放回隨機抽樣，生成 $B = 1,000$ 組合成歷史死亡率路徑：
   $$m_{x,t}^{*(b)} = \widehat{m}_{x,t} \cdot \exp(\epsilon_{x,t}^{*(b)})$$
3. **模型重估與外推**：對每一組重抽數據重新微調 CNN 參數，並向外預測 $T+1, \dots, T+h$。
4. **構建經驗預測分位數**：直接自 1,000 次預測路徑中提取 $\alpha/2$ 與 $1-\alpha/2$ 分位數，生成任意顯著水準的預測區間與扇形圖。

---

## 三、 關鍵實驗成果與評測基準 (Empirical Results & Benchmarks)

1. **跨國數據庫**：人類死亡率資料庫 (HMD) 中 **美國、英國、法國等成熟國家** 歷史死亡率。
2. **點預測精度 (Point Forecast Accuracy)**：
   - 在 10 年與 20 年樣本外回測中，CNN 的均方誤差 (MSE) 不僅全面壓倒 [[李-卡特模型 (Lee-Carter Model)]]，且優於標準多層感知機 (MLP)，展現了二維空間卷積對人口結構的強大歸納偏置（Inductive Bias）。
3. **區間覆蓋率評測 (Interval Coverage Test)**：
   - 檢驗 90% 與 95% 拔靴預測區間的實際落入比例（Empirical Coverage Probability）：
   - 傳統李-卡特隨機游走在長期預測時往往過度擴張或低估極端風險，而 **CNN 拔靴預測區間展現出極高的覆蓋吻合度（95% 信賴區間之實際覆蓋率達到 94.2%~96.1%）**。

---

## 四、 侷限性與批判性反思 (Limitations & Critical Review)

1. **極其龐大的計算開銷**：
   - 為了產出區間預測，必須對深度神經網絡進行 1,000 次重複訓練，對伺服器 GPU 算力要求極高，在即時保單報價系統中難以做到秒級響應。
2. **卷積濾波器的可解釋性仍顯不足**：
   - 儘管卷積核能自動捕捉世代效應，但濾波器權重難以直接轉化為傳統人口學意義明確的 $\kappa_t$ 或 $\gamma_c$ 參數曲線。

---

## 五、 文獻脈絡與演進關係 (Lineage & Related Work)

- **承接自**：[[2018-hainaut-neural-analyzer]]、[[2019-nigri-deep-learning-lc]]、Richman & Wüthrich (2018)。
- **歷史性突破**：
  - **首度成功解決了深度學習在精算長壽風險中「缺乏區間預測」的致命缺陷**，為深度學習通過 Solvency II 資本模型審查開拓了可行的工程範式。
  - 直接啟發了後續 [[2024-qiao-wang-ml-long-term-mortality]] 結合影像鄰域概念進一步開發樹集成模型。
- **跨論文深度對比**：收錄於 [[隨機死亡率模型與機器學習技術演進對比統整]]。
