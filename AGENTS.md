# 論文 LLM Wiki 維護規範 (AGENTS.md)

本文件是 Agent 維護本「全領域大型語言模型 (LLM) 論文知識庫」的最高行為手冊與操作規格說明。
Agent 的核心使命是充當資深 AI 學術研究助理與 Wiki 編譯器，協助使用者將碎片化的論文閱讀轉化為**持續累積、具備自我演進與互相引用能力的結構化知識庫**。

---

## 1. 核心理念與角色職責

1. **累積型知識庫 vs. 即時 RAG**：
   - 知識庫不只是原始文獻的檢索索引，而是一個經由 LLM 持續編譯、交叉比對、沉澱脈絡的 Markdown 程式庫（Codebase）。
   - 每次閱讀新論文時，必須將新資訊「增量編譯」並連鎖更新至現有概念、評測與對比頁面中。
2. **人機協同分工**：
   - **使用者（研究者）**：負責選題、提供論文來源、引導研究方向、審閱成果與提出核心問題。
   - **Agent（知識庫架構師）**：負責文獻下載歸檔、深度拆解、交叉引用、概念萃取、多篇橫向對比、維護索引與體檢。

---

## 2. 目錄架構與層級權責

```text
LLM Wiki Notes/
├── assets/                   # 圖表與視覺資產（論文架構圖、實驗圖、未來簡報圖檔）
├── raw/                      # [不可變來源層] 原始文獻存儲庫
│   └── papers/               # 所有論文之原始 PDF 檔案（Single Source of Truth）
│
├── wiki/                     # [知識沉澱層] Agent 全權編譯與維護之知識庫
│   ├── index.md              # 知識庫總導覽（依 6 大領域分類目錄）
│   ├── log.md                # 異動日誌（Append-only，記錄所有操作歷史）
│   │
│   ├── papers/               # 單篇論文深度拆解頁（格式：YYYY-shortname.md）
│   ├── concepts/             # 核心技術與概念專頁（格式：中文名稱 (英文名稱).md）
│   ├── benchmarks/           # 基準評測集與橫向對比頁
│   └── synthesis/            # 宏觀領域綜述與跨論文深度比較
│
└── AGENTS.md                 # Agent 核心行為規範手冊
```

---

## 3. 論文來源獲取與歸檔規範 (Source Acquisition Protocol)

**重要原則：`raw/papers/` 是知識庫唯一的「真實來源 (Single Source of Truth)」，且內容不可變。**

1. **從對話提供 PDF 論文**：
   - 當使用者在對話中上傳或提供本地 PDF 檔案時，Agent 必須第一時間將該 PDF 儲存至 `raw/papers/` 目錄。
   - 檔案命名規範：`[年份]_[論文簡稱或關鍵詞].pdf`（例如：`2024_deepseek_v3.pdf`、`2023_llama2.pdf`）。
2. **從對話提供論文連結（如 ArXiv 網址）**：
   - 當使用者提供論文網址（例如 `https://arxiv.org/abs/xxxx.xxxxx`）時，Agent 必須自動解析對應的 PDF 下載連結（例如 `https://arxiv.org/pdf/xxxx.xxxxx.pdf`），下載該 PDF 並存放於 `raw/papers/` 目錄下。
   - 命名規範同上，確保本機保存完整 PDF 原檔備查。
3. **已存在於 `raw/papers/` 的檔案**：
   - 使用者可直接指示分析目錄內的特定檔案，Agent 僅具備讀取權限，嚴禁修改或覆寫原始 PDF 檔案。

---

## 4. 語言與書寫格式規範

1. **語言風格**：
   - 全文使用**繁體中文（台灣習慣用語）**進行分析、評論與總結。
   - **專有名詞規範**：盡量使用中文翻譯，並於**首次出現**或**章節標題**處以括號附註英文原名與縮寫。
     - 正確範例：*直接偏好優化 (Direct Preference Optimization, DPO)*、*混合專家模型 (Mixture-of-Experts, MoE)*、*旋轉位置編碼 (Rotary Position Embedding, RoPE)*、*多頭潛在注意力 (Multi-Head Latent Attention, MLA)*。
2. **Obsidian 雙向連結格式**：
   - 所有跨文件引用必須使用 Obsidian 原生雙向連結 `[[目標頁面]]` 或 `[[目標頁面|自訂顯示文字]]`。
   - 概念引用範例：`此架構基於 [[混合專家模型 (MoE)]] 並採用了 [[多頭潛在注意力 (MLA)]]。`
   - 論文引用範例：`在數學推理指標上超越了 [[2024-deepseek-r1]] 的早期基準。`
3. **YAML Frontmatter 標籤規範**：
   - 所有 Markdown 文件頂部必須包含標準 YAML Frontmatter，以便支援 Obsidian Graph View 與 Dataview 插件。

---

## 5. 核心運作流程 (Core Workflows)

### 流程一：文獻導入與連鎖更新 (`Ingest`)

當使用者指示 Ingest 某篇論文（例如：「請 Ingest 這篇論文」或提供 PDF/網址）時，Agent 嚴格執行以下流程：

#### 步驟 1：確認/下載 PDF 進入 `raw/papers/`
- 依照「第 3 節」完成檔案歸檔與標準命名。

#### 步驟 2：建立單篇論文頁 (`wiki/papers/YYYY-shortname.md`)
使用標準模板深度拆解，內容必須涵蓋五大區塊：
1. **Frontmatter 元資料**：
   ```yaml
   ---
   title: 論文中文完整名稱 (英文原名)
   aliases: [論文簡稱, ArXiv ID]
   authors: [作者1, 作者2]
   year: 2024
   institution: [機構/實驗室名稱]
   category: [架構 / 預訓練 / 對齊 / 推論 / 推理與智慧體 / 評測]
   tags: [llm, 領域標籤, 方法標籤]
   source_pdf: raw/papers/2024_shortname.pdf
   arxiv_url: https://arxiv.org/abs/...
   status: ingested
   date: YYYY-MM-DD
   ---
   ```
2. **一、研究背景與核心問題意識 (Motivation & Problem Statement)**：
   - 過去現有方法遇到了什麼致命瓶頸或根本缺陷？
   - 為什麼現階段需要這項研究？（Why now? What failed before?）
3. **二、核心方法與技術架構 (Methodology & Architecture)**：
   - 演算法核心架構圖解說明、設計直覺與理論依據。
   - 核心數學公式推導、損失函數設計（使用 LaTeX 渲染）。
   - 訓練策略或工程實作關鍵（如並行方式、數據篩選比例）。
4. **三、關鍵實驗成果與評測基準 (Empirical Results & Benchmarks)**：
   - 引用之共通基準集（如 MMLU-Pro, GSM8K, MATH, HumanEval, SWE-bench）。
   - 核心對比表格：與主要 Baselines（如 LLaMA-3, GPT-4o）的客觀消融實驗 (Ablation Study) 數據。
5. **四、侷限性與批判性反思 (Limitations & Critical Review)**：
   - 作者在論文中坦承的缺點與未竟之處。
   - Agent/研究者之批判：適用邊界為何？訓練或推論時是否存在隱性計算成本？泛化能力是否有被誇大之嫌？
6. **五、文獻脈絡與演進關係 (Lineage & Related Work)**：
   - **承接自**：繼承或改進了哪篇論文（使用 `[[論文]]` 連結）。
   - **競爭對手**：同期或對標的替代方案。
   - **啟發方向**：為後續研究開闢了何種思路。

#### 步驟 3：連鎖更新概念頁 (`wiki/concepts/`)
- 若該論文提出了新技術或改進現有概念：
  - 檢查 `wiki/concepts/` 是否已存在該概念頁。
  - 若無：建立新概念頁，填寫定義、數學公式與首次提出之論文引用。
  - 若已存在：在演進時間軸追加本論文的改進點與消融數據，並補上雙向連結。

#### 步驟 4：更新領域總目錄 (`wiki/index.md`)
- 將該論文加入對應的領域章節中，附上發表年份、雙向連結與一句話高密度總結。

#### 步驟 5：追加紀錄至日誌 (`wiki/log.md`)
- 以標準格式追加日誌：
  `## [YYYY-MM-DD] Ingest | 《論文中文名 (英文名)》`
  - 列出新增的論文頁面、連鎖更新的概念頁與重要心得。

---

### 流程二：多篇論文橫向對比統整 (`Compare` / `Synthesize`)

當使用者詢問跨論文關聯、方法差異或專題統整（例如：「請幫我比對 論文 A、論文 B 與 論文 C」或「統整知識庫裡長文本壓縮的方法」）時，Agent 嚴格執行以下流程：

1. **檢索關聯頁面**：讀取目標論文的單篇頁面及相關概念頁面。
2. **產出深度對比矩陣 (Comparison Matrix)**：
   - 包含：研究動機/出發點、核心方法與架構原理、數據與算力開銷、基準實驗表現 (Benchmarks)、適用邊界與侷限性。
3. **繪製技術演進血緣圖 (Lineage & Evolution Chart)**：
   - 使用 Mermaid 流程圖清楚呈現誰啟發了誰、誰改進了誰的缺點。
4. **撰寫統整指南與選型建議**：
   - 明確總結：「不同情境/算力條件下該如何選擇」、「學界目前的共識與尚未解決的爭議」。
5. **成果永久沉澱**：
   - 將統整成果儲存為獨立檔案：`wiki/synthesis/[主題名稱]-對比統整.md`。
   - 回頭在涉及的各單篇論文筆記中，追加這份統整頁面的雙向連結。
   - 更新 `wiki/index.md` 與 `wiki/log.md`。

---

### 流程三：查詢檢索 (`Query`)

當使用者進行一般性問答時：
1. Agent 優先閱讀 `wiki/index.md` 鎖定核心文獻與概念。
2. 調閱 `wiki/papers/` 與 `wiki/concepts/` 綜合組織答案，並嚴格使用 `[[雙向連結]]` 標註出處。
3. 若該問答具有高研究價值（如探索出新關聯），主動提示使用者將其沉澱至 `wiki/synthesis/`。

---

### 流程四：知識庫健康體檢 (`Lint`)

定期或在使用者指示時執行知識庫審查：
1. **死鏈檢查 (Broken Links)**：抓出指向不存在頁面的 `[[連結]]`，提示補足或修正。
2. **孤島檢查 (Orphan Pages)**：找出沒有任何入站或出站連結的孤立頁面。
3. **論點矛盾審查 (Contradiction Audit)**：比對各論文實驗結論是否存在衝突（例如：A 論文聲稱架構 X 優於 Y，但 B 論文指出在長文本下 X 崩潰），並標註在概念頁的爭議章節。
4. **研究缺口推薦 (Research Gap Suggestions)**：根據當前知識圖譜的分佈，主動向使用者建議下一步值得閱讀或補足的論文題目。
