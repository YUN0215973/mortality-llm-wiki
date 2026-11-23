---
title: 小區域人口推估研究：臺北市、雲嘉兩縣、澎湖縣的實證分析 (Small Area Population Projection - Empirical Analysis of Taipei City, Yunlin-Chiayi Counties, and Penghu County)
aliases: [Chen & Yue 2010, 小區域人口推估, Taiwan Small Area Projection]
authors: [陳政勳, 余清祥 (Jack C. Yue)]
year: 2010
institution: [國立政治大學統計學系]
journal: 人口學刊, 41, 153–183
category: 人口統計學 / 小區域人口推估 / 拔靴法與相依性建模
tags: [demography, small-area-projection, cohort-component, migration, bootstrap, lee-carter, taiwan-population]
source_pdf: raw/papers/2010_chen_yue_small_area_population.pdf
status: ingested
date: 2026-11-23
---

# 小區域人口推估研究：臺北市、雲嘉兩縣、澎湖縣的實證分析 (Small Area Population Projection: Empirical Analysis of Taipei City, Yunlin-Chiayi Counties, and Penghu County)

> **論文出處**：*人口學刊* (Journal of Population Studies), 第 41 期, 頁 153–183 (2010年12月)  
> **作者**：陳政勳、余清祥  
> **本機存檔**：`raw/papers/2010_chen_yue_small_area_population.pdf`

---

## 一、 研究背景與核心問題意識 (Motivation & Problem Statement)

### 1. 全國性推估掩蓋地方結構失衡的致命缺陷
臺灣歷來的官方人口推估多著眼於全國總體尺度。然而在現實中，城鄉發展差距造成各縣市人口結構急遽分化：
- 都會區（如臺北市）具備強大磁吸效應，青壯人口大量湧入；
- 農業縣市（如雲林縣、嘉義縣）面臨嚴重的青年外移與急速超高齡化；
- 離島地區（如澎湖縣）則受限於地理孤立與特殊醫療交通條件。

### 2. 本文的研究核心動機
地方政府在教育設施（如廢校併校）、醫療長照床位配置及地方稅收財源推估上，亟需具備統計穩健性與隨機信賴區間的「**小區域人口推估 (Small Area Population Projection)**」技術。特別是小區域樣本數較小，隨機波動劇烈，傳統大樣本統計方法容易失真。

---

## 二、 核心方法與技術架構 (Methodology & Architecture)

### 1. 人口要素變動合成法 (Cohort Component Method, CCM)
人口動態基本恆等式：
$$P_{x+1, t+1} = P_{x,t} - D_{x,t} + M_{x,t}$$
新生兒人口：$P_{0, t+1} = B_t + M_{0,t}$，其中 $B_t = \sum_x F_{x,t} W_{x,t}$。
包含三大隨機驅動要素：生育率 ($F$)、死亡率 ($D$) 與淨遷移數 ($M$)。

### 2. 隨機預測與拔靴重抽樣架構 (Bootstrap & Functional PCA)
為了克服小樣本參數估計困難，作者對比了多種前沿推估方法：
- **李-卡特模型 (Lee-Carter Model)** 與 **函數主成份分析 (Functional PCA)**。
- **時間序列拔靴法 (Time Series Bootstrap)**：
  - **區塊拔靴法 (Block Bootstrap)**：將時間序列切分為長度為 $l$ 的連續區塊進行重抽樣，以保留自相關結構。
  - **篩網拔靴法 (Sieve Bootstrap)**：對殘差擬合自迴歸模型後進行白雜訊重抽。
- **相依性假設放寬 (Dependency Modeling)**：
  - 打破傳統推估假設「生育、死亡、遷移三要素互相獨立」的教條，實證分析三者共變異數對未來人口信賴區間的膨脹效應。

---

## 三、 關鍵實驗成果與評測基準 (Empirical Results & Benchmarks)

1. **實證對象**：選取三個代表性相異之行政區進行 1981–2006 歷史資料擬合與樣本外回測：
   - 臺北市（高度都市化都會區）
   - 雲嘉兩縣（人口外流、農村老化區）
   - 澎湖縣（離島孤立型行政區）
2. **方法橫向評估**：
   - 評測指標：均方根百分比誤差 (RMSPE) 與平均絕對百分比誤差 (MAPE)。
   - **實證結論 1**：**區塊拔靴法 (Block Bootstrap)** 在小區域的各項統計指標表現最佳且計算穩健，能有效抵禦異常值干擾。
3. **人口要素實證發現**：
   - **實證結論 2（遷移的決定性角色）**：在全國層級，自然增減（生育與死亡）決定長期趨勢；但在**小區域（縣市層級），「淨遷移 (Net Migration)」是主導未來人口年齡結構變化的最關鍵變數**。
   - **實證結論 3（不確定性區間）**：若考量生育、死亡、遷移間的正相依性，預測的 95% 信賴區間將比傳統獨立假設**擴大 30% 至 50%**，證實低估相依性將嚴重低估地方財政長壽與人口風險。

---

## 四、 侷限性與批判性反思 (Limitations & Critical Review)

1. **外生政策與都市計畫衝擊未參數化**：
   - 純歷史時間序列難以預測重大科學園區進駐、高鐵設站或行政區劃整併帶來的人口驟增。
2. **極高齡小區域數據零膨脹 (Zero-Inflation)**：
   - 離島與偏鄉在 90 歲以上人口暴露數過小，死亡計數出現大量 0，標準常態或卜瓦松假設在此區間需要進一步修勻（如結合 Gompertz 或折扣數列）。

---

## 五、 文獻脈絡與演進關係 (Lineage & Related Work)

- **承接自**：[[2003-yue-taiwan-fertility]]（余清祥臺灣生育率推估）、Lee & Carter (1992)、Smith et al. (2001)。
- **後續影響**：
  - 成為臺灣地方政府與區域精算研究的重要文獻範式，推動了後續臺灣年金與壽險針對不同區域死亡率差異（如城鄉死亡率落差）之實證探討。
- **跨論文深度對比**：收錄於 [[隨機死亡率模型與機器學習技術演進對比統整]]。
