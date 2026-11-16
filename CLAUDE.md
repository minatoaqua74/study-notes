# CLAUDE.md — 期中複習筆記站（study-notes）

> AI 助手請先完整閱讀本文件，再開始修改或新增任何檔案。
> 遇到本文件沒寫到的情況：先參考既有頁面（`notes/unix-basics.html`），保持一致，不要自創風格。

## 1. 專案目的

這是一個「課程複習筆記」靜態網站，用來把各科的考前重點整理成**短、可掃讀、可重複擴充**的網頁。

- 讀者：準備期中／期末考的大學生（作者本人與同學）
- 每個頁面 = 一個主題（例如一個章節或一個考點），閱讀時間 3–5 分鐘
- 目標：之後只要說「幫我新增一頁：〈主題〉」，AI 就能依本文件做出風格一致、可直接發布的頁面

## 2. 技術限制（不可違反）

- 純靜態：**只用 HTML + CSS**，不使用打包工具、框架、npm、建置步驟
- JavaScript 只在真的需要時才加，且寫在頁面底部的 `<script>`，不引入外部函式庫
- 不使用外部 CDN、外部字型、外部圖片（離線也要能開）
- 所有連結使用**相對路徑**（GitHub Pages 的網址有子路徑，絕對路徑 `/` 開頭會壞掉）
- 語言：繁體中文（`<html lang="zh-Hant">`），專有名詞第一次出現時附英文，例如「傳輸層（Transport Layer）」

## 3. 目錄結構

```
study-notes/
├── CLAUDE.md              # 本文件（AI 規則）
├── README.md              # 給人看的專案說明
├── index.html             # 首頁：依科目分組列出所有筆記卡片
├── .nojekyll              # 讓 GitHub Pages 不經 Jekyll 處理
├── assets/
│   └── style.css          # 唯一的樣式表，所有頁面共用
└── notes/
    ├── _template.html     # 新頁面範本（複製它，不要從零寫）
    ├── unix-basics.html   # 範例頁：Unix 基本操作
    └── network-layers.html# 範例頁：網路五層架構
```

## 4. 命名與放置規則

| 項目 | 規則 | 例子 |
|---|---|---|
| 筆記頁檔名 | 英文小寫、單字用 `-` 連接、副檔名 `.html` | `network-layers.html` |
| 放置位置 | 一律放在 `notes/`，不建立子資料夾 | `notes/electronics-diode.html` |
| 範本 | `notes/_template.html` 底線開頭，不出現在首頁 | — |
| 樣式 | 只改 `assets/style.css`，**不在頁面寫 `<style>` 或行內 style** | — |
| 圖片 | 放 `assets/img/`，檔名同頁面名稱加序號，必填 `alt` | `network-layers-1.svg` |

## 5. 新增筆記頁的標準流程

1. 複製 `notes/_template.html` 為 `notes/<kebab-case>.html`
2. 修改 `<title>`、`<h1>`、`data-subject`（科目）、`<meta name="description">`
3. 依第 6 節的頁面結構填入內容（不要刪除或重排區塊）
4. 到 `index.html` 對應科目區塊加一張卡片（格式見第 7 節）；若是新科目，新增一個 `<section class="subject">`
5. 做完自我檢查（第 9 節），再回報修改了哪些檔案

## 6. 頁面結構（每個筆記頁都要有，順序固定）

1. **`<header>`**：返回首頁連結 + `<h1>` 頁面標題 + 科目標籤（`<span class="tag">`）
2. **「一句話重點」**：`<p class="summary">`，不超過 40 字
3. **「核心觀念」**：2–5 個 `<h2>` 小節，每節以短段落或條列呈現，單一段落不超過 4 句
4. **「易錯點／考點」**：`<aside class="warn">`，列出 2–4 個容易錯的地方
5. **「小測驗」**：2–3 題，使用 `<details><summary>題目</summary>答案</details>`，不用 JS
6. **`<footer>`**：上一頁／下一頁（若有）、最後更新日期（`YYYY-MM-DD`）

可用元件（定義在 `style.css`）：`.summary`、`.warn`、`.note`、`.tag`、`<kbd>`、`<pre><code>`、`table`。
需要新元件時：先在 `style.css` 新增 class，並更新本節清單，再使用。

## 6.1 內容撰寫規則

- 內容必須來自使用者提供的講義、習題或課本範圍；**不確定的內容不要編造**，改在頁面中標示 `<aside class="note">待確認</aside>` 並在回報時說明
- 指令與程式碼用 `<pre><code>`，行內指令用 `<code>`
- 數字、公式、協定名稱要精確；若不確定，寧可不寫
- 不複製大段課本或講義原文，用自己的話重點整理

## 7. 首頁卡片格式

```html
<a class="card" href="notes/unix-basics.html">
  <h3>Unix 基本操作</h3>
  <p>使用者管理、sudo、磁碟分割與掛載的重點指令。</p>
  <span class="tag">Unix</span>
</a>
```

- 卡片放在所屬科目的 `<section class="subject">` 內，同科目按學習順序排列
- 卡片簡介一句話，不超過 40 字

## 8. 視覺風格

- 極簡、留白多、以閱讀為主；單欄、最大寬度約 720px
- 色彩只用 `style.css` 的 CSS 變數（`--bg`、`--fg`、`--accent`、`--muted`、`--warn`），支援淺色與深色模式（`prefers-color-scheme`）
- 字體使用系統字型堆疊，不載入外部字型
- 手機優先：必須在 375px 寬度下不出現橫向捲軸

## 9. 完成前自我檢查清單

- [ ] 新頁面可用 `notes/_template.html` 的結構對照，區塊齊全且順序正確
- [ ] 所有連結為相對路徑，且點得到（首頁 → 新頁 → 回首頁）
- [ ] 首頁已新增卡片
- [ ] 沒有外部資源、沒有行內 style、沒有新增 npm 依賴
- [ ] 圖片都有 `alt`；頁面有 `<title>` 與 `<meta name="description">`
- [ ] 有更新「最後更新日期」
- [ ] 回報內容：新增／修改的檔案清單 + 有哪些內容標為「待確認」

## 10. AI 行為規則

- 一次只做被要求的事；不順手重構既有頁面、不改檔名
- 修改既有頁面前先讀完整個檔案，保留原有結構
- 不刪除任何筆記頁，除非使用者明確要求
- 不 commit、不 push，除非使用者明確要求；需要提交時，commit 訊息格式：`add: <頁面名>` / `fix: <說明>` / `docs: <說明>`
- 有疑問就問，不要猜科目範圍或考試範圍

## 11. 部署

- 使用 GitHub Pages：Settings → Pages → Source 選 `Deploy from a branch`，Branch 選 `main`、資料夾 `/ (root)`
- 網址格式：`https://<帳號>.github.io/<repo 名稱>/`
- 推送後約 1–2 分鐘生效；若 404，檢查 `index.html` 是否在 repo 根目錄

## 12. 未來可延伸的方向（目前不做，僅供參考）

- 新增科目：直接新增科目區塊與筆記頁即可，不需改架構
- 新增「考前速查表」頁：沿用同一套元件
- 若頁數超過 20，再討論是否加入搜尋或自動產生首頁（屆時需更新本文件）
