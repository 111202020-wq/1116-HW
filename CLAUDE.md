# CLAUDE.md — Zoe Wu 個人履歷作品集網站

> 這份文件是給 AI（Claude Code、Codex 等）看的「專案說明書」。
> 任何 AI 在修改或新增內容前，**必須先完整讀完本文件**，並依照這裡的規則動手。
> `AGENTS.md` 只是指向本檔的捷徑，規則以本檔為準。

---

## 1. 專案目的

這是吳佩蓁（Zoe Wu，政大國貿系）的**個人履歷作品集網站**，部署在 GitHub Pages。

- **給誰看**：實習／工作面試官、獎學金與交換審查委員、競賽評審。
- **要傳達什麼**：「能把市場數據轉成商業策略、並用簡報說服人」的商管人才，目標是**供應鏈／策略採購**。
- **核心理念**：每一個經歷都要能回答「她做了什麼？成果是什麼？」——所以所有作品頁一律使用 **STAR 結構**（情境 Situation → 任務 Task → 行動 Action → 成果 Result）。

網站的長期用途：之後每多一場競賽、一段實習、一個課堂專案，只要依照本文件「新增作品」流程，就能在幾分鐘內產出風格一致的新頁面。

---

## 2. 技術原則（不可違反）

| 規則 | 說明 |
|---|---|
| 純靜態 | 只用 HTML + CSS + 原生 JavaScript。**不要**引入 React、Vue、Tailwind、npm 套件或建置工具。 |
| 可直接打開 | 所有頁面用瀏覽器直接開 `index.html`（`file://`）也要能正常顯示，所以資料用 `.js` 檔（`window.XXX = ...`），**不要用 `fetch()` 讀 JSON**。 |
| 外部資源 | 只允許 Google Fonts（Noto Sans TC、Noto Serif TC）。不用 CDN 圖示庫，圖示用 inline SVG 或 emoji 以外的文字符號。 |
| 相對路徑 | 所有連結使用相對路徑（GitHub Pages 會放在 `/<repo>/` 子路徑下，絕對路徑 `/` 會壞掉）。 |
| 單一樣式表 | 所有樣式寫在 `assets/css/style.css`，**不要**在 HTML 裡寫 `style=""` 或 `<style>`。 |
| 隱私 | **絕對不可**放入：身分證字號、電話、住址、家庭經濟狀況、獎學金金額、成績單原檔。聯絡方式只放使用者明確同意公開的項目。 |

---

## 3. 檔案結構

```
.
├── CLAUDE.md                 ← 本文件（AI 規則，唯一真相來源）
├── AGENTS.md                 ← 指向 CLAUDE.md 的捷徑
├── README.md                 ← 給人看的專案簡介
├── index.html                ← 首頁：Hero / 關於我 / 能力 / 經歷 / 作品
├── projects/                 ← 每個作品一個 HTML 檔
│   ├── atcc-thsr.html
│   └── spot-ai.html
├── _templates/
│   └── project.html          ← 新增作品時「複製」這個檔案
├── data/
│   ├── profile.js            ← 個人資料、能力、經歷時間軸
│   └── projects.js           ← 作品清單（首頁卡片 & 上下篇導覽的資料來源）
├── assets/
│   ├── css/style.css         ← 唯一的樣式表
│   ├── js/main.js            ← 讀 data/*.js 並渲染首頁與作品頁導覽
│   └── img/                  ← 圖片（依命名規則放置）
├── scripts/
│   └── check.js              ← 規則檢查器：`node scripts/check.js`
└── .nojekyll                 ← 讓 GitHub Pages 不經過 Jekyll 處理
```

**資料與頁面分離**：首頁的「經歷」與「作品卡片」都由 `data/*.js` 渲染，**不要**直接把卡片 HTML 寫死在 `index.html` 裡。

---

## 4. 命名規則

| 對象 | 規則 | 範例 |
|---|---|---|
| 作品 slug | 全小寫英文 + 連字號（kebab-case），2–4 個字，**不含年份** | `atcc-thsr`、`spot-ai`、`garmin-procurement` |
| 作品頁 | `projects/<slug>.html` | `projects/spot-ai.html` |
| 作品圖片 | `assets/img/<slug>/<序號>-<描述>.webp`（或 .jpg/.png） | `assets/img/spot-ai/01-mockup.webp` |
| CSS class | kebab-case，元件前綴：`card-`、`tl-`（timeline）、`star-`、`tag` | `card-title`、`tl-item` |
| 作品類別 `category` | 只能用以下四種之一 | `competition`、`internship`、`leadership`、`coursework` |
| 經歷類型 `type` | 上面四種，再加上 `education`（交換、學歷，只用於時間軸） | `education` |
| 日期 `period` | `YYYY.MM – YYYY.MM`（en dash 前後有空格）或 `YYYY.MM`；**未知時填空字串 `""` 並加 TODO 註解**，不要猜 | `2024.08 – 2025.07` |

類別對應的中文標籤與顏色已定義在 `assets/js/main.js` 的 `CATEGORY_LABELS` 與 CSS 的 `.tag--<category>`。若需新增類別，**兩邊都要加**，並更新本表。

---

## 5. 網頁風格

- **調性**：專業、乾淨、有編輯感（像一份排版精良的商業提案），不要花俏動畫。
- **色彩**（定義在 `style.css` 的 `:root`，**只能用變數，不要寫死色碼**）：
  - `--ink` 深藍黑 #1b2433（主文字）
  - `--paper` 暖白 #faf8f4（背景）
  - `--accent` 赭紅 #c2410c（重點、連結、數字）
  - `--navy` 藏青 #1e3a5f（標題、時間軸）
  - `--muted` 灰 #5b6472（次要文字）
- **字體**：標題用 `Noto Serif TC`（`--font-serif`），內文用 `Noto Sans TC`（`--font-sans`）。
- **數字要突出**：成果數字（名次、金額、百分比）用 `<strong class="metric">` 包起來，會以 accent 色顯示。
- **RWD**：所有版面在 375px 手機寬度下不得出現水平捲軸；格線在 `max-width: 720px` 以下改為單欄。
- **深色模式**：已透過 `prefers-color-scheme: dark` 覆寫變數；新增元件只要用變數就自動支援。

---

## 6. 頁面結構

### 6.1 首頁 `index.html`（區塊順序固定）

1. `#hero`：姓名、一句話定位、主要按鈕（看作品／聯絡）
2. `#about`：自我介紹 2–3 段 + 關鍵數字列（`.stats`）
3. `#skills`：能力分組標籤（資料來自 `profile.js` 的 `skills`）
4. `#experience`：時間軸（資料來自 `profile.js` 的 `experience`，**新到舊**排序）
5. `#projects`：作品卡片網格（資料來自 `projects.js`，依 `order` 排序），可依類別篩選
6. `footer`：聯絡方式 + 最後更新日期

### 6.2 作品頁 `projects/<slug>.html`（必備區塊）

每個作品頁 **必須** 依序包含以下 `id` 的區塊（`scripts/check.js` 會檢查）：

| id | 標題 | 內容要求 |
|---|---|---|
| `summary` | 一句話摘要 | 1–2 句，含最關鍵成果數字 |
| `situation` | 情境 Situation | 背景、市場或組織的問題 |
| `task` | 任務 Task | 我要解決什麼、我的角色 |
| `action` | 行動 Action | 具體做了哪些事，**用條列**，每點以動詞開頭 |
| `result` | 成果 Result | 量化成果，使用 `.metric` |
| `reflection` | 我學到什麼 | 2–4 句，連結到未來目標（供應鏈／採購） |

另外：
- `<body>` 必須有 `data-page="project"` 與 `data-slug="<slug>"`，`main.js` 會據此自動產生「上一篇／下一篇」。
- 頁首 `.project-meta` 列出：時間、角色、團隊、成果（四格）。
- 所有引用到首頁或素材的連結都以 `../` 開頭。

---

## 7. 新增內容的標準流程（AI 必須照做）

### 7.1 新增一個作品

1. 決定 slug（依第 4 節規則）。
2. 複製 `_templates/project.html` → `projects/<slug>.html`。
3. 取代模板中所有 `{{...}}` 佔位符；**完成後檔案中不可殘留 `{{`**。
4. 在 `data/projects.js` 的陣列中新增一筆物件，欄位如下（全部必填，`image` 可為 `null`）：
   ```js
   {
     slug: "garmin-procurement",
     title: "Garmin 採購實習",
     category: "internship",          // 見第 4 節
     period: "2025.07 – 2025.12",     // 格式：YYYY.MM – YYYY.MM 或 YYYY.MM
     role: "採購實習生",
     summary: "一句話（≤ 60 字），含成果數字",
     highlight: "協調 6 家供應商",     // 卡片上的大字成果（≤ 12 字）
     tags: ["採購", "庫存管理"],       // 2–4 個
     image: null,
     order: 3                          // 數字越小越前面
   }
   ```
5. 若此作品對應一段經歷，同步更新 `data/profile.js` 的 `experience`（加上 `link: "projects/<slug>.html"`）。
6. 執行 `node scripts/check.js`，**必須全部通過**才算完成。
7. 更新 `index.html` footer 的「最後更新」日期（`<time id="updated">`）。

### 7.2 新增一段經歷（不需獨立頁面）

只編輯 `data/profile.js` 的 `experience` 陣列，維持新到舊排序；欄位：`period`、`title`、`org`、`desc`、`type`（同 category）、`link`（可選）。

### 7.3 修改個人資料／能力

只編輯 `data/profile.js`。**不要**為了改文字去動 `main.js`。

---

## 8. 寫作規範

- 語言：**繁體中文為主**，專有名詞、課程名、公司名保留英文（如 Operations Management、Garmin）。
- 中英文之間加半形空格：「在 Garmin 擔任採購實習生」。
- 數字一律用阿拉伯數字，名次寫成「第 1 名」「Top 16/219」。
- 用第一人稱「我」，語氣自信但具體；**禁止空泛形容詞**（如「非常優秀」「很有熱忱」）而沒有事實支撐。
- 不捏造：所有數字與經歷必須來自使用者提供的資料。資料不足時，在頁面中留下 `<!-- TODO: 需要使用者補充 XXX -->` 並在回覆中告知使用者，**不要自行編造**。

---

## 9. AI 修改時的禁止事項 & 檢查清單

**禁止**
- 刪除或改名既有的 `id`、CSS 變數、`data/*.js` 欄位名稱（會讓其他頁面壞掉）。
- 在 `projects/*.html` 內手寫上一篇／下一篇連結（由 `main.js` 產生）。
- 新增第二個 CSS 檔或 inline style。
- 放入第 2 節列出的隱私資料。

**完成前檢查**
- [ ] `node scripts/check.js` 全部通過
- [ ] 用瀏覽器打開首頁與新頁面，桌機與手機寬度（375px）都正常
- [ ] 新卡片出現在首頁、點擊可進入、上下篇導覽正確
- [ ] footer 更新日期已修改
- [ ] commit 訊息格式：`feat(project): 新增 <slug>`、`fix: ...`、`docs: ...`、`style: ...`

---

## 10. 部署

- 推送到 `main` 分支後，GitHub Pages（Settings → Pages → Deploy from branch → `main` / `root`）會自動更新。
- 網址：`https://5jhen.github.io/<repo-name>/`
