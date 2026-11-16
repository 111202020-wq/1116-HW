# 吳佩蓁 Zoe Wu — 個人履歷作品集

政大國貿系吳佩蓁的個人履歷作品集網站，使用純 HTML / CSS / JavaScript，部署在 GitHub Pages。

🔗 網站：https://5jhen.github.io/1116-HW/

## 特色

- **STAR 作品頁**：每個競賽／實習都以「情境 → 任務 → 行動 → 成果」呈現
- **資料驅動**：經歷時間軸與作品卡片由 `data/*.js` 渲染，改資料不必動版面
- **AI 友善**：[`CLAUDE.md`](./CLAUDE.md) 定義完整規則，AI 可依規則快速新增頁面
- **自動檢查**：`node scripts/check.js` 驗證必備區塊、命名、隱私等規則

## 新增一個作品（3 步驟）

1. 複製 `_templates/project.html` → `projects/<slug>.html`，填入內容
2. 在 `data/projects.js` 新增一筆資料
3. 執行 `node scripts/check.js` 確認通過

或直接對 AI 說：「依照 CLAUDE.md 新增一個作品：Garmin 採購實習……」

## 本機預覽

直接用瀏覽器打開 `index.html` 即可（不需要伺服器）。
