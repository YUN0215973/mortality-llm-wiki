---
title: 臺灣地區生育率推估方法的研究 (A Comparison of Fertility Projection Methods - A Case Study in Taiwan Area)
aliases: [Yue 2003, 臺灣生育率推估, Taiwan Fertility Projection]
authors: [余清祥 (Jack C. Yue)]
year: 2003
institution: [國立政治大學統計學系]
journal: 人口學刊, 26, 145–171
category: 人口統計學 / 生育率模型 / 參數與時間序列推估
tags: [demography, fertility-projection, lee-carter, taiwan-population, time-series, asfr]
source_pdf: raw/papers/2003_yue_taiwan_fertility_projection.pdf
status: ingested
date: 2026-11-23
---

# 臺灣地區生育率推估方法的研究 (A Comparison of Fertility Projection Methods: A Case Study in Taiwan Area)

> **論文出處**：*人口學刊* (Journal of Population Studies), 第 26 期, 頁 145–171 (2003年6月)  
> **作者**：余清祥 (Jack C. Yue)  
> **本機存檔**：`raw/papers/2003_yue_taiwan_fertility_projection.pdf`

---

## 一、 研究背景與核心問題意識 (Motivation & Problem Statement)

### 1. 臺灣生育率雪崩式下滑的歷史背景
臺灣地區在二十世紀後半葉經歷了全球罕見的超快速人口轉型：
- 總生育率 (Total Fertility Rate, TFR) 自 1961 年的 **5.58** 劇降至 1983 年的替代水準 (2.1)，2001 年更跌破 **1.4**（四十年內下滑逾 70%）。
- 官方行政院經建會傳統推估長期沿用「高、中、低推計」的主觀定值假設，面臨嚴重系統性高估未來出生人口的窘境。

### 2. 本文研究核心痛點
人口推估為社會保險、國民年金、學校教育資源與勞動力規劃之基石，但相較於死亡率具備穩定向下之生物醫學趨勢，**年齡別生育率 (Age-Specific Fertility Rate, ASFR)** 受到經濟波動、結婚年齡延後與生育觀念轉變之強烈干擾。本文旨在系統性評估將經典隨機模型引入臺灣生育率推估之可行性與精確度。

---

## 二、 核心方法與技術架構 (Methodology & Architecture)

本文將生育率推估模型劃分為兩大體系進行橫向評估：

### 1. 參數化生育曲線模型 (Parametric Fertility Models)
利用年齡分佈的非對稱單峰特性擬合年齡別生育率 $f(x)$：
- **哈德威格函數 (Hadwiger Function)**：
  $$f(x) = \frac{a b}{c \sqrt{\pi}} \left(\frac{c}{x - d}\right)^{3/2} \exp\left\{ -b^2 \left( \frac{c}{x - d} + \frac{x - d}{c} - 2 \right) \right\}$$
  其中 $d$ 為生育年齡下限，$a$ 為總和生育率比例因子，$b, c$ 決定曲線峰度與偏度。
- **伽瑪密度函數 (Gamma Function)** 與 **Beta 函數** 曲線擬合。

### 2. 李-卡特隨機時間序列架構 (Lee-Carter Adapted for Fertility)
借鑒 [[李-卡特模型 (Lee-Carter Model)]] 將年齡別對數生育率矩陣進行雙線性奇異值分解 (SVD)：
$$\ln f_{x,t} = a_x + b_x k_t + \epsilon_{x,t}$$
- $a_x = \frac{1}{T} \sum_t \ln f_{x,t}$：各生育年齡（15–49 歲）之歷史基準生育輪廓。
- $k_t$：捕捉跨年代生育水準整體變化的時間綜合指數，約束 $\sum_t k_t = 0$。
- $b_x$：特定年齡對時期生育率變化的敏感度權重，約束 $\sum_x b_x = 1$。
- **外推機制**：以單變量自迴歸整合移動平均模型 $\text{ARIMA}(p,d,q)$（如隨機游走漂移過程）對 $k_t$ 進行預測外推。

---

## 三、 關鍵實驗成果與評測基準 (Empirical Results & Benchmarks)

1. **實證數據**：臺灣地區 1971–2000 年育齡婦女（15–49 歲）年齡別生育率。
2. **樣本外預測回測評估**：
   - 以均方根誤差 (RMSE) 與平均絕對誤差 (MAE) 進行 5–10 年外推檢定。
   - **實證結論**：隨機型 [[李-卡特模型 (Lee-Carter Model)]] 搭配 $\text{ARIMA}(1,1,0)$ 的外推精確度全面超越傳統 Hadwiger 與 Gamma 靜態參數模型。
3. **生育高峰後移（晚育現象）之捕捉**：
   - 模型成功辨識出臺灣婦女生育高峰自 20–24 歲向 25–29 歲甚至 30–34 歲推移的結構性延後（Tempo Effect）。

---

## 四、 侷限性與批判性反思 (Limitations & Critical Review)

1. **對數雙線性假設對生育率的結構性偏誤**：
   - 死亡率的年齡形狀 $\beta_x$ 在跨年代間相對平穩，但生育率的年齡形貌（峰值位置與分散程度）在超低生育率轉型期發生劇烈扭曲，單一固定向量 $b_x$ 難以完全吸收生育延後（Tempo Effect）與育齡壓縮（Quantum Effect）的雙重變動。
2. **缺乏社會經濟與婚姻狀態變數**：
   - 純時間序列模型無法解釋女性勞動參與率上升、房價、育兒津貼政策等外在結構衝擊。

---

## 五、 文獻脈絡與演進關係 (Lineage & Related Work)

- **承接自**：Lee & Carter (1992)、Lee (1993)、Hadwiger (1940)。
- **啟發臺灣在地人口研究**：
  - 開啟了將現代隨機時間序列引進臺灣人口推估之先河，奠定了後續 [[2010-chen-yue-small-area-population]]（小區域人口推估）、[[2014-wang-yue-marriage-mortality]]（婚姻與死亡率）與 [[2019-lee-liu-taiwan-mortality-models]] 的方法論基礎。
- **跨論文深度對比**：收錄於 [[隨機死亡率模型與機器學習技術演進對比統整]]。
