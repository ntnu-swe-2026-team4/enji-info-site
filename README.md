# Enji 反詰式對話教室 - 詳細操作指南

蘇格拉底對話教室（Enji · 詰問）的使用說明網站。內容依照實際操作畫面整理，分成「開始使用」、「老師」、「學生」、「設定與常見問題」四個部分，帶第一次使用的人一步一步上手。

- **網站**：[https://ntnu-swe-2026-team4.github.io/enji-info-site/](https://ntnu-swe-2026-team4.github.io/enji-info-site/)
- **Source Repo**：[ntnu-swe-2026-team4/socrates-classroom](https://github.com/ntnu-swe-2026-team4/socrates-classroom)

## 檔案結構

```
.
├── index.html        # 整份使用說明（HTML + 內嵌 CSS，沒有 JavaScript、沒有建置步驟）
└── assets/
    └── guide/        # 說明中用到的操作截圖（800×500 JPG）
```

網站是單一靜態頁面，直接用瀏覽器打開 `index.html` 就能看。字型（Noto Sans TC、Noto Serif TC、DotGothic16）從 Google Fonts 載入，離線時會退回系統字型。

## 本機預覽

```bash
python3 -m http.server 8000
# 打開 http://localhost:8000
```

## 視覺風格

沿用 socrates-classroom 首頁與登入頁的漫畫網點風格，只有淺色版：

| 項目 | 值 |
| --- | --- |
| 墨色 | `#0b0b0b` |
| 深色底（頁首、Hero） | `#202022` |
| 金色（主要按鈕） | `#c4ae7d` |
| 朱紅（重點、焦點框） | `#c1302a` |
| 網點底 | `#f3f3f1` 底 + `#cfcfcb` 12px 圓點 |
| 標題字 | Noto Serif TC |
| 內文字 | Noto Sans TC |
| 小標、編號 | DotGothic16 |

按鈕 hover 用和 app 相同的「下沉」效果（`translate: 2px 2px` 加內側陰影）。顏色都定義在 `index.html` 開頭的 `:root` 變數裡，改色從那裡改。

## 撰寫慣例

- 介面上的按鈕名稱用 `<span class="ui">按鈕</span>` 標示，app 中的主要（金色）按鈕加 `pri`：`<span class="ui pri">開始活動</span>`。
- 鍵盤按鍵用 `<kbd>`。
- 提示與注意事項用 `<div class="tip"><b>提示</b>…</div>`。
- 每張截圖都要寫 `alt` 文字與 `figcaption`。
- 按鈕與功能名稱以 app 實際畫面上的文字為準。

## 部署與 CI/CD

- **CI**（`.github/workflows/ci.yml`）：於 PR 與 `main` push 時執行 `yamllint` 檢查 workflow，並驗證 `index.html` 的本地資源路徑、內部錨點、圖片 `alt` 屬性與子路徑相容性。
- **CD**（`.github/workflows/pages.yml`）：推送到 `main`（或手動觸發 `workflow_dispatch`）時自動透過 GitHub Actions 部署至 GitHub Pages。其他靜態主機（Cloudflare Pages、Netlify 等）也只需要把整個資料夾上傳，不需要建置指令。
