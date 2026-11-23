# 知識庫異動日誌 (Activity Log)

## [2026-11-23] discuss | 建立 Wiki 前的討論（2026-11-23 補記）
- 主題：建立死亡率機器學習與深度學習知識庫、PDF 論文導入、跨篇比較與簡報製作
- 受眾：使用者（研究者）
- 範圍：收錄使用者於本次對話上傳的全部 PDF 論文（共 10+ 份）
- 頁面格式：每篇論文頁包含 Frontmatter、研究背景、核心方法、實驗成果、限制與文獻脈絡等段落（參考 AGENTS.md 指南）
- 決定事項：
  - 將 PDF 存入 `raw/papers/` 並建立相應的 wiki 頁面
  - 以表格與卡片方式比較模型（Lee‑Carter、Random Forest/GBDT、CNN、LSTM、Auto‑Encoder）
  - 產出 HTML slide 簡報（V2、V3）

本檔案為 append-only 格式之時間軸日誌，記錄 Agent 針對知識庫執行的所有 Ingest（導入）、Compare/Synthesize（對比統整）與 Lint（體檢）操作。

---

## [2026-11-23] Initialize | 知識庫初始化與架構建立
- **操作類型**：系統建置
- **完成項目**：
  - 建立三層式目錄結構：`raw/papers/`、`wiki/papers/`、`wiki/concepts/`、`wiki/benchmarks/`、`wiki/synthesis/`。
  - 制定並寫入最高行為規範手冊 `AGENTS.md`。
  - 初始化總導覽索引 `wiki/index.md` 與本異動日誌 `wiki/log.md`。
- **備註**：知識庫已就緒，可開始接收 PDF 檔案或論文連結進行導入。


## [2026-11-23] Ingest | 《基於樹模型之機器學習死亡率建模與預測 (Tree-Based Machine Learning Methods for Modeling and Forecasting Mortality)》
- **來源歸檔**：`raw/papers/2022_tree_based_mortality.pdf`（本機 PDF 歸檔）
- **單篇頁面**：[[2022-tree-based-mortality]]
- **連鎖新增概念**：
  - [[模式信賴集合 (Model Confidence Set, MCS)]]
  - [[隨機梯度提升 (Stochastic Gradient Boosting)]]
  - [[隨機森林 (Random Forests)]]
  - [[李-卡特模型 (Lee-Carter Model)]]
- **核心實證貢獻**：
  - 證實純樹狀機器學習模型（Pure GB / Pure RF）在對數死亡率一階差分轉換下，預測表現顯著優於 9 種傳統隨機死亡率模型（如李-卡特、CBD、Plat）及其殘差混合模型。
  - 推翻過去文獻宣稱「殘差樹模型必勝」的論點，指出傳統模型加裝機器學習殘差在退休年齡段 (59–89) 反而劣於純傳統模型。
  - 提出可解釋性剖析工具（PDP、`inTrees` 決策規則），成功從 3,200 個分裂條件中自動挖掘出 1969 年香港流感及東歐華沙公約國家的死亡停滯特徵。


## [2026-11-23] Ingest Batch | 批量導入 9 篇精算隨機死亡率模型與機器學習前沿論文
- **來源歸檔**：
  - `raw/papers/2002_brouhns_poisson_lc.pdf`
  - `raw/papers/2006_cairns_two-factor_cbd.pdf`
  - `raw/papers/2006_renshaw_haberman_cohort.pdf`
  - `raw/papers/2007_cairns_comparison_stochastic.pdf`
  - `raw/papers/2012_ohare_li_young_mortality.pdf`
  - `raw/papers/2018_hainaut_neural_analyzer.pdf`
  - `raw/papers/2019_levantesi_pizzorusso_ml.pdf`
  - `raw/papers/2019_nigri_deep_learning_lc.pdf`
  - `raw/papers/2020_levantesi_longevity_ml.pdf`
- **新增單篇頁面**：
  - [[2002-brouhns-poisson-lc]]：卜瓦松對數雙線性迴歸極大概似估計 (MLE) 標準範式。
  - [[2006-cairns-two-factor-cbd]]：高齡二因子對數勝算比模型 (CBD / M5)。
  - [[2006-renshaw-haberman-cohort]]：李-卡特世代效應擴展模型 (RH / M2)。
  - [[2007-cairns-comparison-stochastic]]：M1~M8 隨機模型量化比較與 M7 最佳穩健架構。
  - [[2012-ohare-li-young-mortality]]：延伸 CBD 二次曲線之全年齡模型 (M10)。
  - [[2018-hainaut-neural-analyzer]]：神經網絡自編碼器非線性主成份分析 (NLPCA)。
  - [[2019-levantesi-pizzorusso-ml]]：隨機森林與梯度提升擬合傳統模型殘差之兩階段混合架構。
  - [[2019-nigri-deep-learning-lc]]：長短期記憶網路 (LSTM) 取代 ARIMA 預測時間指數。
  - [[2020-levantesi-longevity-ml]]：機器學習於長壽風險管理文獻綜述。
- **連鎖新增核心概念專頁**：
  - [[長短期記憶網路 (Long Short-Term Memory, LSTM)]]
  - [[世代效應 (Cohort Effect)]]
  - [[長壽風險 (Longevity Risk)]]
  - [[通用年齡-時期-世代模型 (GAPC)]]


## [2026-11-23] Synthesize | 《隨機死亡率模型與機器學習技術演進對比統整》
- **操作類型**：跨論文多篇深度對比與知識綜述沉澱
- **產出專頁**：[[隨機死亡率模型與機器學習技術演進對比統整]]
- **核心沉澱內容**：
  - 統整精算科學 30 年間三大範式轉移：古典 GAPC 統計體系 $\rightarrow$ 殘差混合學習 $\rightarrow$ 純機器學習與深度序列記憶。
  - 繪製 10 篇論文演進關係之 Mermaid 流程血緣圖。
  - 建立 10 篇論文之全維度橫向對比矩陣（動機、架構、數據集、評測結論、局限性與邊界）。
  - 深入剖析四大核心學術爭端：純 ML vs. 殘差混合、高齡年金 vs. 全年齡、ARIMA vs. LSTM、黑盒可解釋性與 Solvency II 監理審計。
  - 產出精算實務決策樹與業務選型指南（年金險、法定資本計提、商業前瞻定價）。
- **連鎖更新**：
  - 回溯更新 10 篇論文筆記之雙向連結。
  - 更新總目錄 [[index|wiki/index.md]]。


## [2026-11-23] Ingest Batch | 批量導入第二批 10 篇論文與補充附錄
- **檔案重命名與規範化歸檔**：
  - `Machine Learning in Long-term Mortality Forecasting.pdf` $\rightarrow$ `raw/papers/2024_qiao_wang_ml_long_term_mortality.pdf`
  - `Machine learning techniques for mortality modeling.pdf` $\rightarrow$ `raw/papers/2017_deprez_ml_mortality_modeling.pdf`
  - `Mortality Health and Marriage A Study Based on Taiwans Population Data.pdf` $\rightarrow$ `raw/papers/2014_wang_yue_marriage_mortality.pdf`
  - `On stochastic mortality modeling.pdf` $\rightarrow$ `raw/papers/2009_plat_stochastic_mortality.pdf`
  - `point-and-interval-forecasts-of-death-rates-using-neural-networks.pdf` $\rightarrow$ `raw/papers/2021_schnurch_korn_neural_networks.pdf`
  - `小區域人口推估研究：臺北市、雲嘉兩縣、澎湖縣的實證分析.pdf` $\rightarrow$ `raw/papers/2010_chen_yue_small_area_population.pdf`
  - `死亡率模型之比較：以臺灣資料為例.pdf` $\rightarrow$ `raw/papers/2019_lee_liu_taiwan_mortality_models.pdf`
  - `臺灣地區生育率推估方法的研究.pdf` $\rightarrow$ `raw/papers/2003_yue_taiwan_fertility_projection.pdf`
  - `規律折扣數列與高齡死亡率.pdf` $\rightarrow$ `raw/papers/2011_wang_yue_discount_sequence.pdf`
  - `附錄A-TREE-BASEDMACHINELEARNINGMETHODS...pdf` $\rightarrow$ `raw/papers/2022_bjerre_tree_mortality_appendix_a.pdf`（作為 `[[2022-tree-based-mortality]]` 補充附錄資料）
  - `高齡死亡率模型的探討.pdf` $\rightarrow$ `raw/papers/2016_wang_yue_old_age_mortality.pdf`
- **新增單篇論文深度拆解頁**：
  - [[2003-yue-taiwan-fertility]]：余清祥臺灣年齡別生育率隨機時間序列推估。
  - [[2009-plat-stochastic-mortality]]：Richard Plat 融匯 LC 與 CBD 之經典全年齡 M9 模型。
  - [[2010-chen-yue-small-area-population]]：陳政勳與余清祥小區域人口推估與區塊拔靴法。
  - [[2011-wang-yue-discount-sequence]]：王信忠與余清祥開創之博弈論規律折扣數列與高齡 DSW 模型。
  - [[2014-wang-yue-marriage-mortality]]：王信忠與余清祥臺灣婚姻狀態死亡率實證（差距超越吸菸風險）。
  - [[2016-wang-yue-old-age-mortality]]：王信忠等人高齡關係模型 (DSW) 與隨機模型之跨國大規模評估。
  - [[2017-deprez-ml-mortality-modeling]]：Philippe Deprez 等人精算機器學習樹狀提升死亡率之開山之作。
  - [[2019-lee-liu-taiwan-mortality-models]]：李永琮等人臺灣隨機死亡率模型比較與非常態厚尾分配 (NIG)。
  - [[2021-schnurch-korn-neural-networks]]：Simon Schnürch 與 Ralf Korn 2D CNN 死亡率影像視角與拔靴區間預測。
  - [[2024-qiao-wang-ml-long-term-mortality]]：喬洋、王昭文、朱文君空間-世代鄰域特徵與雙重樹集成 SOTA 模型。
- **連鎖新增核心概念專頁**：
  - [[折扣數列模型 (Discount Sequence Model, DS 與 DSW)]]
  - [[卷積神經網路於死亡率預測 (Convolutional Neural Networks for Mortality, CNN)]]
  - [[小區域人口推估 (Small Area Population Projection)]]
- **更新既有概念專頁**：
  - 連鎖更新 [[通用年齡-時期-世代模型 (GAPC)]] 納入 M9 Plat 模型與 Deprez 機器學習診斷。


## [2026-11-23] Synthesize Expansion | 全景擴充《隨機死亡率模型與機器學習技術演進對比統整》
- **操作類型**：跨 20 篇核心論文全圖譜橫向對比升級
- **產出專頁**：[[隨機死亡率模型與機器學習技術演進對比統整]]
- **核心更新內容**：
  - 擴充為涵蓋國際古典 GAPC、臺灣本土人口與精算實證、機器學習樹模型、深度神經網絡之四大分支演進架構。
  - 重新繪製 20 篇文獻全血緣之 Mermaid 關係圖。
  - 擴充 20 篇論文之全維度橫向對比大矩陣。
  - 深入剖析五大核心學術爭端（純 ML vs. 殘差 ML、高齡 DSW vs. GAPC、點預測 vs. 區間估計、2D CNN vs. 表格樹集成、西方模型 vs. 臺灣急遽老化人口）。
  - 完善精算實務決策樹與模型選型指南。
- **連鎖更新**：
  - 更新總目錄 [[index|wiki/index.md]]（目前論文總數：20 篇，核心概念：11 個，統整專頁：1 篇）。

## [2026-11-23] slides | 簡報 v9：依 20 篇論文頁重寫，一篇一卡；依 PDF 更正生育率論文年份、DSW 歸屬、2019 女性最佳模型；統整頁與論文頁矛盾處改採論文頁
