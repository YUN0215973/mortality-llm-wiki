---
title: 長壽風險 (Longevity Risk)
aliases: [Longevity Risk, 系統性長壽風險, 聚合長壽風險]
category: 精算科學 / 風險管理
tags: [actuarial-science, risk-management, longevity-risk, annuities, pensions, capital-requirement]
date: 2026-11-23
---

# 長壽風險 (Longevity Risk)

> **定義**：在精算科學與金融風險管理中，「長壽風險」指特定人群的實際平均餘命系統性超越預期，導致終身年金（Annuities）、確定給付制退休基金（Defined-Benefit Pension Funds）與長期照護保險的給付現值大幅增加，進而威脅發行機構償付能力之財務風險。

---

## 一、 風險本質：個體微觀波動 vs. 總體系統性風險

精算上必須嚴格區分兩種不同維度的壽命風險：
1. **個別獨立風險 (Idiosyncratic Longevity Risk)**：
   - 指個別保單持有人過世時點的不確定性。
   - **特性**：服從大數法則（Law of Large Numbers），保險公司可透過擴大承保池（Pooling）實現風險分散（Diversification）。
2. **總體/聚合長壽風險 (Aggregate / Systemic Longevity Risk)**：
   - 指整個人口群體在醫療進步、生活品質改善或公共衛生突破下，整體死亡率趨勢改善幅度超出歷史定價預期。
   - **特性**：無法透過單純擴大承保池分散；若整批被保險人平均多活 1 年，年金負債將全體膨脹，屬於不可分散的系統性金融風險。

---

## 二、 精算負債與資本衝擊評估

### 1. 終身年金現值公式
年齡 $x$ 歲之個人即期終身年金現值（Actuarial Present Value, APV）：
$$a_x = \sum_{k=1}^\infty (1+r)^{-k} \cdot {}_k p_x$$
其中：
- $r$ 為折現率（Interest rate）。
- ${}_k p_x = \prod_{j=0}^{k-1} (1 - q_{x+j, t+j})$ 為存活至 $x+k$ 歲之累積存活機率。
- **敏感度分析**：實務統計顯示，退休年齡群體之死亡率若每年多下降 1%，年金負債總現值約增加 3% 至 5%。

### 2. 監理資本要求 (Solvency II & IFRS 17)
- 歐盟償付能力二號 (Solvency II) 規定，保險機構必須針對長壽風險提存償付能力資本要求 (SCR)，標準法假設未來死亡率瞬間永久下降 20%。
- 內模法（Internal Models）則要求建置具備完整不確定性分佈（Full Stochastic Distribution）之死亡率動態模型，模擬 99.5% 1年 VaR。

---

## 三、 長壽風險的避險與資本市場轉移工具 (Capital Market Solutions)

傳統再保險市場承保容量有限，催生了長壽衍生性金融商品的發展：
1. **長壽債券 (Longevity Bonds)**：
   - 2004 年由歐洲投資銀行 (EIB) 與法國巴黎銀行 (BNP Paribas) 發行，票息給付直接與 65 歲人口存活率指數掛鉤。
2. **長壽交換合約 (Longevity Swaps)**：
   - 退休基金定期向避險交易對手（投資銀行或再保險公司）支付預先約定的固定金額（Fixed leg），換取交易對手支付退休人員實際發生的浮動年金給付（Floating leg）。
3. **死亡率遠期合約 (q-Forwards)**：
   - 針對特定年齡群體在未來特定年份之死亡率 $q_{x,t}$ 簽訂的遠期結算合約。
4. **基差風險 (Basis Risk)**：
   - 衍生性商品結算通常基於國家官方人口指數（如 HMD 全國人口），而避險機構自身的被保險人族群在社經地位、生活型態上與全國人口存在差異，產生的未對沖殘差即為基差風險。

---

## 四、 機器學習與人工智慧在長壽風險管理之演進

如 [[2020-levantesi-longevity-ml]] 所統整，現代計算技術對長壽風險管理的推進歷經三大範式：
1. **古典隨機死亡率模型**：
   - 以 [[李-卡特模型 (Lee-Carter Model)]]、CBD (2006) 為代表，透過降維與 ARIMA 產出均值與閉式預測區間。
   - **弱點**：難以捕捉多維非線性互動，容易低估模型不確定性。
2. **混合殘差學習 (Hybrid Residual Learning)**：
   - 以 [[2019-levantesi-pizzorusso-ml]] 為代表，利用 [[隨機森林 (Random Forests)]] 與 [[隨機梯度提升 (Stochastic Gradient Boosting)]] 擬合經典模型濾波後的非線性殘差，改善邊界擬合。
3. **深度神經網絡與序列學習 (Deep Sequence Learning)**：
   - 以 [[2018-hainaut-neural-analyzer]]（自編碼器降維）與 [[2019-nigri-deep-learning-lc]]（[[長短期記憶網路 (Long Short-Term Memory, LSTM)]] 預測時間指數）為代表，大幅提升長期外推精度。
4. **點預測 vs. 風險量化之落差**：
   - 機器學習與深度學習目前大多聚焦於提高「點預測 (Point Forecast)」的 RMSE/MAPE 精度，然而精算風險管理（如 Solvency II 資本計提）核心需求為「整條尾端機率分佈 (Tail Risk Quantile)」。未來需結合拔靴法 (Bootstrapping) 或貝氏神經網絡 (Bayesian Neural Networks) 產出預測信賴區間。

---

## 五、 相關文獻與交叉引用

- [[2006-cairns-two-factor-cbd]]：專門為高齡長壽風險定價設計之二因子隨機死亡率模型。
- [[2007-cairns-comparison-stochastic]]：針對英格蘭與美國年金數據評估不同隨機死亡率模型之長壽風險預測表現。
- [[2020-levantesi-longevity-ml]]：回顧機器學習於長壽風險管理中扮演的角色與未來挑戰。
- [[2019-nigri-deep-learning-lc]]：利用 LSTM 降低長壽風險預測之均方誤差。
- [[2022-tree-based-mortality]]：利用機器學習特徵可解釋性解析歷史死亡率驟降背後的結構轉變。
- [[通用年齡-時期-世代模型 (GAPC)]]：長壽風險動態預測之統一建模架構。
