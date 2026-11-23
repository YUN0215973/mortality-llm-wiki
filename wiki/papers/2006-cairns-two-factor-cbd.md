---
title: 具參數不確定性之隨機死亡率雙因子模型：理論與校正 (A Two-Factor Model for Stochastic Mortality with Parameter Uncertainty: Theory and Calibration)
aliases: [CBD Model, Cairns 2006, CBD 2006, Model M5]
authors: [Andrew J. G. Cairns, David Blake, Kevin Dowd]
year: 2006
institution: [英國赫瑞-瓦特大學 (Heriot-Watt University), 倫敦城市大學卡斯商學院 (Cass Business School), 諾丁漢大學]
journal: Journal of Risk and Insurance, 73(4), 687–718
category: 隨機死亡率模型 / 長壽債券定價 / 風險中立定價
tags: [actuarial-science, stochastic-mortality, cbd-model, longevity-risk, parameter-uncertainty, risk-neutral-pricing, longevity-bonds]
source_pdf: raw/papers/2006_cairns_two_factor_cbd.pdf
doi: 10.1111/j.1539-6975.2006.00195.x
status: ingested
date: 2026-11-23
---

# 具參數不確定性之隨機死亡率雙因子模型：理論與校正 (A Two-Factor Model for Stochastic Mortality with Parameter Uncertainty)

> **論文出處**：*Journal of Risk and Insurance*, 73(4), 687–718. DOI: [10.1111/j.1539-6975.2006.00195.x](https://doi.org/10.1111/j.1539-6975.2006.00195.x)  
> **作者**：Andrew J. G. Cairns, David Blake, Kevin Dowd  
> **本機存檔**：`raw/papers/2006_cairns_two_factor_cbd.pdf`

---

## 一、 研究背景與核心問題意識 (Motivation & Problem Statement)

### 1. 金融化長壽風險對沖的迫切需求
隨著年金受益人預期壽命大幅超過預期，保險公司與退休基金面臨沉重財務壓力。2004 年 11 月，歐洲投資銀行 (EIB) 與法國巴黎銀行 (BNP Paribas) 發行了全球首檔 25 年期「長壽債券 (Longevity Bond)」，其息票給付直接掛鉤英國英格蘭與威爾斯 65 歲男性世代的存活率指標 $S(t)$。如何對此類包含隨機死亡風險與長跨度期限的金融商品進行嚴謹定價，成為當時學界最重要的挑戰。

### 2. 現有死亡率模型的不足
1. **李-卡特 (Lee-Carter) 模型是單因子**：所有年齡層的死亡率變動完全共線，無法反映高齡層與低齡層死亡率改善速度不同的結構性傾斜 (Tilt)。
2. **忽略參數不確定性 (Parameter Uncertainty)**：傳統定價往往將校正出的參數視為已知常數，嚴重低估了 10~25 年超長天期合約的尾部風險。
3. **缺乏風險調整測度架構**：金融工程需要自「真實世界測度 $\mathbb{P}$」轉換至「風險調整測度 $\mathbb{Q}$」的定價橋樑。

---

## 二、 核心方法與技術架構 (Methodology & Architecture)

### 1. 雙因子 Logit 死亡率曲線模型 (CBD 核心結構 / M5)
CBD 模型針對 60 歲以上的高齡死亡率，將死亡機率 $q(t, x)$ 的 Logit 轉換設定為年齡的線性函數：

$$\text{logit}\, q(t, x) = \ln \left( \frac{q(t, x)}{1 - q(t, x)} \right) = A_1(t+1) + A_2(t+1)(x+t)$$

在標準化年齡表記法下（令 $\bar{x}$ 為樣本平均年齡）：
$$\text{logit}\, q(t, x) = \kappa_t^{(1)} + \kappa_t^{(2)} (x - \bar{x})$$

- **第一因子 $\kappa_t^{(1)}$（水平位移因子 Level Factor）**：對全體年齡層產生等量影響，描述總體死亡率隨時間下降的基準水平。
- **第二因子 $\kappa_t^{(2)}$（斜率/旋轉因子 Slope Factor）**：隨年齡呈線性遞增，捕捉高齡族群與年輕族群死亡改善速率的差異（改善曲線的變陡趨勢）。

### 2. 雙變量隨機漫步動態
狀態變數向量 $A(t) = (A_1(t), A_2(t))'$ 遵循二維帶有漂移項的隨機漫步過程：
$$A(t+1) = A(t) + \mu + C Z(t+1)$$
其中 $Z(t) \sim \mathcal{N}(0, I_2)$，$V = CC'$ 為共變異數矩陣（$C$ 為 Cholesky 上三角矩陣分解）。

### 3. 貝氏法納入參數不確定性 (Parameter Uncertainty)
作者採用 Jeffrey 非資訊先驗分佈 $p(\mu, V) \propto |V|^{-3/2}$，推導出後驗分佈為**常態-逆威夏特分佈 (Normal-Inverse-Wishart Distribution)**：
$$V^{-1} \mid D \sim \text{Wishart}(n-1, n^{-1} \widehat{V}^{-1})$$
$$\mu \mid V, D \sim \mathcal{MVN}(\widehat{\mu}, n^{-1}V)$$
模擬時先抽取 $(V, \mu)$，再沿路徑生成隨機漫步，完整體現估計誤差對長天期存活指數的擴散效應。

### 4. 風險中立定價測度 $\mathbb{Q}(\lambda)$
在不完全市場下，建立實質測度 $\mathbb{P}$ 至風險調整測度 $\mathbb{Q}$ 的測度轉換：
$$A(t+1) = A(t) + \widetilde{\mu} + C \widetilde{Z}(t+1), \quad \text{其中 } \widetilde{\mu} = \mu - C \lambda$$
$\lambda = (\lambda_1, \lambda_2)'$ 為長壽風險的市場價格 (Market Prices of Longevity Risk)。
債券在市場無套利下的公允定價為：
$$V_\lambda(0) = \sum_{T=1}^{25} P(0, T) \mathbb{E}_{\mathbb{Q}(\lambda)}[S(T) \mid \mathcal{M}_0]$$

---

## 三、 關鍵實驗成果與評測基準 (Empirical Results & Benchmarks)

1. **數據擬合**：英國英格蘭與威爾斯 1961–2002 年 60 歲以上男性人口數據。
2. **參數風險的爆發性影響**：
   - 在預測前 10 年內，存活率變異數非常小。
   - **在第 25 年時，參數不確定性佔了存活指標 $S(t)$ 總變異數的將近一半 ($50\%$)**！若忽略參數風險，金融機構將嚴重低估保險負債儲備金。
3. **EIB 長壽債券隱含風險貼水校正**：
   - 根據 EIB 債券發行利率低於 LIBOR 35 個基點（折合年化長壽風險貼水約 $\delta = 20$ 個基點），反推市場長壽風險價格：$(\lambda_1, \lambda_2) \approx (0.175, 0.175)$。
   - 世代起始年齡越老（如 70 歲世代 vs 60 歲世代），對應的長壽風險貼水越高（70 歲 30 年期債券風險貼水高達 42.3 bps）。

---

## 四、 侷限性與批判性反思 (Limitations & Critical Review)

1. **專為高齡設計，無法泛化至全年齡**：CBD 模型假設 Logit 死亡率隨年齡呈純線性，這在 60 歲以上極為精確，但若套用到 60 歲以下，因無法擬合青少年意外突起 (Accident Hump) 而完全崩潰（促成後續 Plat 2009 與 [[2012-ohare-li-young-mortality]] 的產生）。
2. **原始版本未包含世代效應 (Cohort Effect)**：促成作者在後續研究擴展為 M6 (加世代)、M7 (加二次年齡項與世代)、M8 (世代遞減)。

---

## 五、 文獻脈絡與演進關係 (Lineage & Related Work)

- **承接自**：Perks (1932) 羅吉斯死亡率定律、Milevsky & Promislow (2001) 隨機存活定價。
- **與李-卡特流派的競爭**：成為精算界除了李-卡特 (Lee-Carter) 之外**最著名的兩大主流學派之一（CBD 家族）**。
- **啟發後續工作**：[[2007-cairns-comparison-stochastic]] 建立之 M5~M8 體系、Plat (2009) 混合模型，以及當代長壽衍生性金融商品定價。
- **跨論文深度對比**：收錄於 [[隨機死亡率模型與機器學習技術演進對比統整]]，探討 CBD 高齡專用架構相對於全年齡與機器學習模型之權衡。
