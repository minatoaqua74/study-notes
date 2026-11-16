# 期中複習筆記站（study-notes）

一個純 HTML + CSS 的靜態網站，把課程考前重點整理成「每頁一個主題、3–5 分鐘讀完」的筆記。

- 網頁：`https://<帳號>.github.io/<repo 名稱>/`
- AI 規則：見 [`CLAUDE.md`](CLAUDE.md)（結構、命名、頁面格式、檢查清單）

## 目前內容

| 科目 | 頁面 |
|---|---|
| Unix | `notes/unix-basics.html` |
| 網路通訊概論 | `notes/network-layers.html` |

## 新增頁面

對 AI 說「幫我新增一頁：〈主題〉」，並提供講義或重點。AI 會依 `CLAUDE.md`：

1. 複製 `notes/_template.html`
2. 填入內容
3. 在 `index.html` 加卡片
4. 逐項檢查後回報

## 本機預覽

直接用瀏覽器開啟 `index.html` 即可，不需要任何建置工具。
