---
title: 李-卡特模型之世代效應擴展與死亡率下降因子研究 (A cohort-based extension to the Lee–Carter model for mortality reduction factors)
aliases: [Renshaw-Haberman Model, RH Model, RH 2006, Model M2]
authors: [A. E. Renshaw, S. Haberman]
year: 2006
institution: [英國倫敦城市大學卡斯商學院 (Cass Business School)]
journal: Insurance: Mathematics and Economics, 38(3), 556–570
category: 隨機死亡率模型 / 世代效應 / 廣義非線性模型
tags: [actuarial-science, stochastic-mortality, lee-carter, cohort-effect, mortality-reduction-factor, gnm]
source_pdf: raw/papers/2006_renshaw_haberman_cohort.pdf
doi: 10.1016/j.insmatheco.2005.12.001
status: ingested
date: 2026-11-23
---

# 李-卡特模型之世代效應擴展與死亡率下降因子研究 (A cohort-based extension to the Lee–Carter model)

> **論文出處**：*Insurance: Mathematics and Economics*, 38(3), 556–570. DOI: [10.1016/j.insmatheco.2005.12.001](https://doi.org/10.1016/j.insmatheco.2005.12.001)  
> **作者**：A. E. Renshaw, S. Haberman  
> **本機存檔**：`raw/papers/2006_renshaw_haberman_cohort.pdf`

---

## 一、 研究背景與核心問題意識 (Motivation & Problem Statement)

### 1. 英國人口統計中顯著的「黃金世代效應 (Golden Cohort)」
英國精算局與政府精算部 (GAD) 歷次人口普查發現一個特殊現象：出生於 **1925 至 1945 年之間（特別是 1931 年前後出生）的世代**，其一生的死亡率改善速度遠高於之前或之後出生的族群。這種沿著出生年份對角線傳播的現象即為「**世代效應 (Cohort Effect)**」。

### 2. 經典李-卡特模型的致命失真
經典 [[李-卡特模型 (Lee-Carter Model)]]（包括 [[2002-brouhns-poisson-lc]] 的卜瓦松改良版）本質上是「年齡-時期 (Age-Period)」雙維度模型。當應用於英國等具有強烈世代特徵的數據時：
- 殘差圖沿著出生年份出現顯著的**波紋狀群聚 (Ripple Effects)**，嚴重違反隨機誤差的 i.i.d. 獨立同分佈假設。
- 忽略世代效應會系統性低估年金受領人的預期壽命，造成龐大的保險準備金缺口。

---

## 二、 核心方法與技術架構 (Methodology & Architecture)

### 1. 廣義非線性世代擴展模型 (RH 模型 / Model M2)
作者在死亡力結構中引入額外的年齡-世代雙線性相乘項：

$$\mu_{x,t} = \exp\left( \alpha_x + \beta_x^{(0)} \iota_{t-x} + \beta_x^{(1)} \kappa_t \right)$$

在 mortality reduction factor 框架下表示為：
$$\ln F(x, t) = \beta_x^{(0)} \iota_{t-x} + \beta_x^{(1)} \kappa_t$$

- $\alpha_x$：基準年齡效應（生命表基準）。
- $\kappa_t$：時期指數 (Period Index)，描述時間推移下的總體死亡改善。
- $\beta_x^{(1)}$：各年齡對時期改善的敏感度。
- $\iota_{t-x}$（常記為 $\gamma_{t-x}$）：**世代指數 (Cohort Index)**，以出生年份 $z = t - x$ 為索引，捕捉特定世代終生享有的死亡改善溢價。
- $\beta_x^{(0)}$：**年齡對世代效應的調節權重**。

### 2. 模型約束與兩階段估計法
為確保參數唯一可識別性 (Identifiability)，施加約束條件：
$$\sum_x \beta_x^{(0)} = 1, \quad \sum_x \beta_x^{(1)} = 1, \quad \iota_{t_1 - x_k} = 0 \quad (\text{或 } \kappa_{t_1} = 0)$$

採用卜瓦松誤差結構與兩階段迴歸：
1. 第一階段由對數死亡率時間均值估計基準 $\widehat{\alpha}_x$。
2. 第二階段利用 GLIM 或單維牛頓法疊代估計雙線性項 $(\beta_x^{(0)}, \iota_{t-x}, \beta_x^{(1)}, \kappa_t)$。

### 3. 時間序列雙重外推 (Time Series Projections)
外推時需同時建立兩組獨立的 ARIMA 模型：
- 對時期參數 $\kappa_t$ 建立 ARIMA(1,1,0) 或 ARIMA(2,1,0)。
- 對世代參數 $\iota_z$ 建立單變量 ARIMA(1,1,0) 進行向前遞迴預測。

---

## 三、 關鍵實驗成果與評測基準 (Empirical Results & Benchmarks)

1. **數據集**：英格蘭與威爾斯 1961–2003 全體人口死亡資料（年齡 0–99 歲男女分開）。
2. **殘差波紋完全消除**：
   - 相比於李-卡特 (LC) 模型殘差圖中劇烈的世代傾斜條紋，RH 模型成功消除了殘差相關性，殘差隨機均勻分佈。
3. **世代曲線歷史印記驗證**：
   - 世代指數 $\widehat{\iota}_z$ 在 1918 一戰結束（含西班牙大流感）與 1945 二戰結束處出現顯著的結構斷裂。
   - 1925–1945 世代的 $\widehat{\iota}_z$ 出現陡峭下降，實證佐證了黃金世代的快速長壽增長。
4. **年金現值估算大幅翻升**：
   - 65 歲即期年金現值 $a_{65}(t)$（以 5% 固定利率計算）：在納入世代效應後，**預測年金現值顯著高於傳統李-卡特模型**，證實忽略世代效應將造成保險業者定價嚴重偏低。

---

## 四、 侷限性與批判性反思 (Limitations & Critical Review)

1. **嚴重的數值不穩定性與弱識別問題 (Identifiability Issues)**：
   - 本文提出的模型在實務估計時收斂極慢，目標概似函數在局部極值處極度平坦。
   - 後續研究（如 Currie 2006、[[2007-cairns-comparison-stochastic]]、Hunt & Villegas 2015）指出：**RH 模型對擬合的時間區間非常敏感**（用 1961–2000 數據與 1981–2000 數據校正出的參數形態出現根本性劇變），缺乏參數穩健性 (Robustness)。
2. **為簡化版 APC 鋪路**：由於 $\beta_x^{(0)}$ 估計過於波動，後續 Currie (2006) 建議強行固定 $\beta_x^{(0)} = 1$ 與 $\beta_x^{(1)} = 1$，轉為標準的加法型 APC 模型。

---

## 五、 文獻脈絡與演進關係 (Lineage & Related Work)

- **承接自**：[[李-卡特模型 (Lee-Carter Model)]]、[[2002-brouhns-poisson-lc]]、Willets (2004)。
- **被評測與改進**：在 [[2007-cairns-comparison-stochastic]] 中被編列為 **Model M2**，在 BIC 指標上名列前茅，但穩健性被嚴重質疑；[[2019-levantesi-pizzorusso-ml]] 將其納為混合樹模型之重要基礎。
- **跨論文深度對比**：收錄於 [[隨機死亡率模型與機器學習技術演進對比統整]]，分析世代效應引入後之數值收斂挑戰與模型演進。
