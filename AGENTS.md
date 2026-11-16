# AGENTS.md

本專案的 AI 開發規則統一寫在 [`CLAUDE.md`](./CLAUDE.md)。

任何 AI agent（Codex、Cursor、Claude Code 等）在修改本專案前，請**先完整閱讀 `CLAUDE.md`**，並遵守其中的：

1. 技術原則（純靜態、無建置工具、相對路徑、隱私限制）
2. 檔案結構與命名規則
3. 作品頁 STAR 必備區塊
4. 新增內容的標準流程（複製 `_templates/project.html` → 登錄 `data/projects.js` → 執行 `node scripts/check.js`）

快速指令：

```bash
node scripts/check.js   # 檢查所有規則是否通過
```
