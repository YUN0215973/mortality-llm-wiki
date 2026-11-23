---
title: 神經網路分析器於死亡率預測之應用 (A neural-network analyzer for mortality forecast)
aliases: [Hainaut 2018, Neural Network Analyzer, NLPCA Mortality]
authors: [Donatien Hainaut]
year: 2018
institution: [比利時法語天主教魯汶大學 (UCL) 統計、生物統計與精算科學研究所]
journal: Astin Bulletin, 48(2), 481–508
category: 深度學習死亡率預測 / 非線性主成分分析 / 自編碼器
tags: [machine-learning, deep-learning, neural-networks, autoencoder, nlpca, lee-carter, mortality-forecasting]
source_pdf: raw/papers/2018_hainaut_neural_analyzer.pdf
doi: 10.1017/asb.2017.45
status: ingested
date: 2026-11-23
---

# 神經網路分析器於死亡率預測之應用 (A neural-network analyzer for mortality forecast)

> **論文出處**：*Astin Bulletin*, 48(2), 481–508. DOI: [10.1017/asb.2017.45](https://doi.org/10.1017/asb.2017.45)  
> **作者**：Donatien Hainaut  
> **本機存檔**：`raw/papers/2018_hainaut_neural_analyzer.pdf`

---

## 一、 研究背景與核心問題意識 (Motivation & Problem Statement)

### 1. 傳統主成分分析 (PCA) 的線性邊界
在以 [[李-卡特模型 (Lee-Carter Model)]] 及其多因子擴展（Renshaw & Haberman 2003）為代表的隨機死亡率模型中，核心估計步驟皆高度依賴奇異值分解 (SVD) 或主成分分析 (PCA) 來抽取時間潛在因子 $\kappa_t$。

然而，PCA 在理論上具有一個致命前提：**僅能有效擷取高斯線性結構**。一旦死亡率曲面存在複雜的非線性特徵（如醫療技術突破、流行病衝擊、不同年齡層改善速率的非線性扭曲），PCA 將完全喪失偵測能力，導致重構的死亡率曲面失真。

### 2. 機器學習早期研究的缺陷
過去少數將神經網路應用於死亡率的研究，多僅將神經網路作為計量迴歸的直接替代品，無法生成涵蓋全年齡與未來長天期的完整死亡率期限結構 (Term Structure of Mortality)，無法用於實際的精算資產負債管理與年金定價。

---

## 二、 核心方法與技術架構 (Methodology & Architecture)

### 1. 非線性主成分分析 (NLPCA) 與瓶頸神經網路架構
作者引入 Kramer (1991) 的非線性主成分分析 (NLPCA)，構建一套**「編碼器-瓶頸-解碼器 (Autoencoder)」神經網路架構**：

```mermaid
flowchart LR
    X["輸入層 X(t) ∈ R^nx<br>(中心化對數死亡率向量)"] --> H1["編碼隱藏層 R^nl<br>(雙曲正切激勵 φ_sig)"]
    H1 --> B["瓶頸瓶頸層 R^d<br>(線性激勵，萃取 d 個潛在因子 κ_t^nn)"]
    B --> H2["解碼隱藏層 R^nl<br>(雙曲正切激勵 φ_sig)"]
    H2 --> X_hat["輸出重構層 X^(t) ∈ R^nx<br>(重構對數死亡率曲面)"]
```

- **編碼階段 (Encoding)**：
  $$y_{i,1}(t) = \varphi_{sig}\left( \sum_{k=1}^{n_x} \omega_{i,k}^1 X_k(t) \right), \quad \kappa_t^{nn,i} = \sum_{k=1}^{n_l} \omega_{i,k}^2 y_{k,1}(t)$$
- **解碼階段 (Decoding)**：
  $$\ln \mu(t, x) = \alpha_x + f^{dec}(x, \kappa_t^{nn})$$
  取代了傳統李-卡特中生硬的線性乘積 $\alpha_x + \beta_x \kappa_t$，賦予模型任意逼近非線性平面的能力（通用逼近定理）。

### 2. 遺傳演算法 (GA) 與梯度下降的兩階段混合優化
由於死亡率跨年齡矩陣維度極高（輸入年齡多達 90 個），標準反向傳播梯度下降極易陷入局部極值 (Local Minima)。
- **第一階段：遺傳演算法 (Genetic Algorithm, GA)**：透過 100 組候選染色體、洗牌交配 (Shuffle/Arithmetic Crossover)、模擬退火變異 (Mutation) 與菁英主義錦標賽，進行全域搜索。
- **第二階段：梯度下降 (Gradient Descent)**：以 GA 最佳解為起始點進行微調。

### 3. 潛在時間因子隨機漫步外推
瓶頸層抽取的潛在時間因子 $\kappa_t^{nn}$ 呈現高度平滑的準線性趨勢，經 Jarque-Bera (JB) 統計檢定證實符合常態性假設，可直接採用多元隨機漫步 (Random Walk with Drift) 進行未來長天期模擬。

---

## 三、 關鍵實驗成果與評測基準 (Empirical Results & Benchmarks)

1. **數據集**：法國、英國與美國人口死亡率數據（校正期 1946–2000，驗證期 2001–2014）。
2. **預測誤差大幅下降 (法國數據 2001–2014 外推驗證)**：
   - 傳統多因子 SVD 李-卡特模型：預測平方誤差和 (SSE) 為 **$38.37$**。
   - 具世代效應之 RH 模型 (LC COH)：預測 SSE 為 **$17.65$**。
   - **3–2–3 神經分析器 (本文模型)**：預測 SSE 暴跌至 **$8.17$**（**誤差比世代李-卡特降低超過 53%**）！
3. **過擬合 (Overfitting) 的實證警示**：
   - 測試 3–2–3 至 8–3–8 各種結構發現：雖然 8–3–8 在訓練期擬合誤差最低，但外推預測誤差卻最高（SSE 升至 17.43）。證實**神經網路在精算建模中必須嚴格控制神經元數量以防過擬合**。
4. **非對稱長壽分佈特徵**：神經網路模擬出的未來死亡率分佈呈現右偏與厚尾 (Leptokurtic)，更貼近歷史真實分佈，修正了傳統高斯分佈低估極端長壽風險的盲點。

---

## 四、 侷限性與批判性反思 (Limitations & Critical Review)

1. **年齡分組邊界不連續 (Cut-off Artifaces)**：為減少參數量，作者將年齡分成 3 個獨立輸入神經元，導致在 50 歲分界點附近的預測誤差出現不自然跳躍。
2. **缺乏即時信賴區間閉式解**：點預測精確度極高，但信賴區間必須仰賴 10,000 次龐大的蒙地卡羅模擬。

---

## 五、 文獻脈絡與演進關係 (Lineage & Related Work)

- **承接自**：[[李-卡特模型 (Lee-Carter Model)]]、Kramer (1991) NLPCA、McNelis (2005)。
- **啟發後續**：作為精算界第一篇將深度自動編碼器引入死亡率期限結構預測的奠基之作，直接啟發了後續 [[2019-nigri-deep-learning-lc]]（LSTM 時間序列化）與 Richman & Wüthrich (2018)。
- **跨論文深度對比**：收錄於 [[隨機死亡率模型與機器學習技術演進對比統整]]，探討自編碼器非線性降維在精算模型圖譜中之定位。
