---
title: 小區域人口推估 (Small Area Population Projection)
aliases: [Small Area Population Projection, 縣市層級人口推估, 地方人口推估]
category: 人口學 / 統計推估 / 區域精算
tags: [demography, small-area, population-projection, cohort-component, migration, bootstrap, taiwan-population]
date: 2026-11-23
---

# 小區域人口推估 (Small Area Population Projection)

> **定義**：在人口統計學與精算科學中，「小區域人口推估」指針對國家以下之次級行政區（如縣市、鄉鎮市區、都會核心區或偏遠離島）進行未來人口規模、性別比例與年齡結構之推計。其核心挑戰在於小區域人口基數小、隨機波動劇烈，且人口動態往往不由自然增減（出生與死亡）主導，而是由**「人口遷移（Migration）」**起決定性作用。

---

## 一、 小區域推估與全國性推估之本質差異

| 維度 | 全國層級人口推估 (National Level) | 小區域人口推估 (Small Area Level) |
| :--- | :--- | :--- |
| **主導驅動要素** | 生育率與死亡率（自然增減） | **國內淨遷移與社會遷移（社會增減）** |
| **數據統計特性** | 大數法則成立，隨機波動平滑 | 樣本數小，波動劇烈，高齡層常出現零死亡計數 |
| **要素獨立性** | 傳統多假設生育、死亡、遷移相互獨立 | **各要素間存在高度空間相關與社會經濟相依性** |
| **外生政策敏感度** | 國家總體公衛與經濟政策影響漸進 | 地方產業園區設廠、交通高鐵建設、學區變動引發瞬間劇變 |

---

## 二、 核心技術架構：人口要素變動合成法 (Cohort Component Method)

小區域推估的核心基石為年齡世代遞移方程式：
$$P_{x+1, t+1} = P_{x,t} - D_{x,t} + M_{x,t}$$
其中：
- $P_{x,t}$：年齡 $x$ 於年份 $t$ 的期初存活人口。
- $D_{x,t}$：該年齡組死亡人數，通常透過 [[李-卡特模型 (Lee-Carter Model)]] 或平滑關係模型預測。
- $M_{x,t}$：淨遷移人口（Net Migration），為小區域模型最關鍵且難度最高的外推變數。

### 拔靴重抽樣法的引入 (Bootstrap Techniques)
如 [[2010-chen-yue-small-area-population|陳政勳與余清祥 (2010)]] 所示，小區域推估常引進時間序列拔靴法：
1. **區塊拔靴法 (Block Bootstrap)**：保留歷史序列的局部自相關與跨要素共變異數，避免參數分佈假設失真。
2. **放寬相依性假設**：實證指出，若將生育、死亡與遷移視為正相依變數，未來推估之信賴區間將大幅擴張，能更真實反映地方長照與學校整併之財務安全邊際。

---

## 三、 相關文獻與交叉引用

- [[2010-chen-yue-small-area-population]]：臺灣小區域人口推估（臺北市、雲嘉、澎湖）之經典實證研究。
- [[2003-yue-taiwan-fertility]]：臺灣年齡別生育率隨機時間序列推估基礎。
- [[2014-wang-yue-marriage-mortality]]：探討次族群（婚姻狀態）人口結構之死亡率異質性。
- [[李-卡特模型 (Lee-Carter Model)]]：小區域死亡率與生育率外推常用之 Baseline 隨機模型。
