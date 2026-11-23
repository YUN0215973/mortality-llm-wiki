---
title: 長期死亡率預測之機器學習新框架 (Machine Learning in Long-term Mortality Forecasting)
aliases: [Qiao, Wang & Zhu 2024, 鄰域特徵機器學習, NSYSU 2024]
authors: [喬洋 (Yang Qiao), 王昭文 (Chou-Wen Wang), 朱文君 (Wenjun Zhu)]
year: 2024
institution: [國立中山大學財務管理學系, 新加坡南洋理工大學南洋商學院]
category: 現代機器學習 / 長期死亡率預測 / 鄰域效應與樹集成 / 多人口遷移學習
tags: [actuarial-science, machine-learning, tree-boosting, ensemble-learning, neighborhood-effect, long-term-forecasting, multi-population, longevity-risk]
source_pdf: raw/papers/2024_qiao_wang_ml_long_term_mortality.pdf
status: ingested
date: 2026-11-23
---

# 長期死亡率預測之機器學習新框架 (Machine Learning in Long-term Mortality Forecasting)

> **論文出處**：學術前沿研究手稿 / 預印本 (2024).  
> **作者**：喬洋 (Yang Qiao)、王昭文 (Chou-Wen Wang, 國立中山大學財管系特聘教授)、朱文君 (Wenjun Zhu, 新加坡南洋理工大學)  
> **本機存檔**：`raw/papers/2024_qiao_wang_ml_long_term_mortality.pdf`

---

## 一、 研究背景與核心問題意識 (Motivation & Problem Statement)

### 1. 超長程死亡率預測（20–30年）的維度災難
在壽險年金定價、長期照護保險與社會保障基金精算中，往往需要跨越 **20 至 30 年的超長期死亡率外推**：
- **傳統 GAPC 模型的收縮與發散問題**：經典模型（如 Lee-Carter 與 CBD）在外推至 20 年以上時，常出現各年齡死亡率改善幅度人為收縮（Half-shrinking pattern）或趨勢單調直線發散的弊病。
- **孤立預測忽視空間關聯**：傳統模型在預測特定年齡 $x$ 時，難以靈活調用相鄰年齡（$x-1, x+1$）與相鄰出生世代的局部動態關聯。

### 2. 深度學習與樹狀模型的優劣權衡
- 深度神經網路（如 [[2021-schnurch-korn-neural-networks|CNN]] 與 [[2019-nigri-deep-learning-lc|LSTM]]）雖具備高維非線性能力，但在樣本量有限的人口數據上調參困難、極易過擬合；
- 樹狀模型（如 [[2022-tree-based-mortality|Bjerre 2022]] 證實之純樹模型）具備強大穩定度與可解釋性，但傳統特徵工程尚未充分整合「空間鄰域動態資訊」。

---

## 二、 核心方法與技術架構 (Methodology & Architecture)

本文提出一套整合「**鄰域效應 (Neighborhood Effect)**」、「**樹狀提升 (Tree Boosting)**」、「**模型整合 (Model Ensembling)**」與「**多人口遷移學習 (Multi-Population Learning)**」的全新機器學習預測框架：

### 1. 空間-世代鄰域特徵工程 (Neighborhood Feature Engineering)
借鑒影像處理與卷積概念，為目標年齡 $x$ 與年份 $t$ 顯式構建局部鄰域特徵矩陣：
- **年齡鄰域 (Age Neighborhood)**：納入相鄰年齡窗口 $[x - k, x + k]$ 的歷史死亡率改善率；
- **世代鄰域 (Cohort Neighborhood)**：沿著對角線軌跡提取出生世代窗口 $[(t-x) - l, (t-x) + l]$ 的改善動能；
- 透過跨年齡與跨世代的局部梯度特徵，徹底消除長程外推中的人為收縮現象。

### 2. 梯度樹提升與雙重集成 (Tree Boosting & Ensemble Architecture)
- 基礎學習器採用先進的梯度提升樹架構（XGBoost / LightGBM / CatBoost）；
- **雙重集成機制 (Bagging + Boosting)**：在 Boosting 序列迭代之上，再疊加 Bootstrap 抽樣集成，大幅壓低長期外推時累積的預測變異數。

### 3. 多人口遷移學習 (Multi-Population Transfer Learning)
突破單一國家數據量的限制，將多個地理、經濟相近國家的人口歷史數據並行輸入，讓模型在第一階段先學習跨國通用的總體醫療技術進步與流行病特徵，第二階段再微調至目標國家，解決小人口國家的長程預測失真問題。

---

## 三、 關鍵實驗成果與評測基準 (Empirical Results & Benchmarks)

1. **實證數據集**：人類死亡率資料庫 (HMD) 跨多個大洲、不同人口規模之歷史數據（涵蓋 20 年至 30 年超長預測回測期）。
2. **長程預測精確度大幅躍升 (MAPE)**：
   - 評測指標：平均絕對百分比誤差 (MAPE) 與均方根誤差 (RMSE)。
   - **實證結論 1**：在 **20 年超長期預測期** 中，本文框架相較於以 Lee-Carter 為代表的經典隨機死亡率模型，**MAPE 降低了將近 30% 至 50%**。
   - **實證結論 2（超越深度學習基準）**：在面對多國不同資料特徵時，本文的「鄰域特徵 + 樹集成」架構在泛化穩定性與樣本效率上，**顯著擊敗了基於 CNN 與 LSTM 的深度學習對標模型**。
   - **實證結論 3（多人口借力效應）**：納入跨國多人口數據後，目標國家的長期預測誤差進一步下降 10%–15%，驗證了跨國遷移學習之有效性。

---

## 四、 侷限性與批判性反思 (Limitations & Critical Review)

1. **超參數網格搜索成本高**：
   - 鄰域窗口寬度 ($k, l$)、學習率、樹深度與集成數量交織構成龐大的超參數搜索空間，需依賴嚴格的滾動驗證防範過度擬合。
2. **多人口數據對齊要求嚴格**：
   - 多人口聯合訓練仰賴各國 HMD 統計口徑的高度一致性，若納入戰亂或統計不全的非成熟國家可能引入資料污染。

---

## 五、 文獻脈絡與演進關係 (Lineage & Related Work)

- **承接自**：[[2017-deprez-ml-mortality-modeling]]、[[2021-schnurch-korn-neural-networks]]（空間鄰域概念）、[[2022-tree-based-mortality]]（純樹模型長程差分預測）。
- **學術前沿地位**：
  - **代表了 2024 年當前精算科學中機器學習長程死亡率預測的最高水準 (State-of-the-Art)**；
  - 成功結合了臺灣學者（中山大學王昭文團隊）在精算財務與機器學習的前沿洞見，展示了樹模型在吸收影像鄰域思想後的巨大威力。
- **跨論文深度對比**：收錄於 [[隨機死亡率模型與機器學習技術演進對比統整]]。
