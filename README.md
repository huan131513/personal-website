# personal-website

一頁式個人網站（light theme），單一 `index.html`，零建置、零依賴。

## 本地預覽

直接用瀏覽器開啟 `index.html`，或起一個本機伺服器：

```bash
python3 -m http.server 4321
```

## 響應式斷點

| 寬度 | 行為 |
| --- | --- |
| `< 400px` | 統計數字縮排、卡片內距縮小 |
| `< 640px` | CTA 按鈕滿版、光暈模糊度降低（省效能） |
| `< 720px` | 作品單欄 |
| `< 860px` | 導覽列收成漢堡選單 + 全螢幕面板 |
| `720–999px` | 作品 2 欄 + 最後一張跨滿版 |
| `≥ 980px` | 技能 4 欄 |
| `≥ 900px` | 關於我變成「側欄 + 內文」兩欄 |
| `≥ 1500px` | 內容區加寬到 1160px |

另外還處理了橫向短螢幕（`max-height:520px`）、`hover:none` 觸控裝置（拿掉 hover-only 效果）、
`env(safe-area-inset-*)` 瀏海機、以及列印樣式。字級與間距用 `clamp()` 流體縮放，斷點之間也不會突兀。

## 動態效果

- 頂端捲動進度條、捲動後才浮現的導覽底線與返回頂端按鈕
- Hero 背景三顆漂浮光暈（aurora blobs）+ 顆粒質感
- 標題漸層流動、職稱文字每 2.6 秒輪播
- 數字捲到畫面內才 count-up
- 區塊進場淡入，子元素依序 stagger
- 技術標籤無限跑馬燈（hover 暫停）
- 作品卡片跟隨游標的 3D 傾斜與光暈（只在精準指標裝置啟用）
- 全部包在 `prefers-reduced-motion` 底下，使用者關閉動效就直接顯示最終狀態

## 要改的地方

| 位置 | 內容 |
| --- | --- |
| `<title>` / `<meta name="description">` / og tags | SEO 與分享預覽 |
| `.hero` | 名字、`#roles` 輪播職稱、狀態徽章（不需要就刪掉 `.badge`） |
| `.stats` | `data-count` 是目標數字、`data-suffix` 是後綴 |
| `.marquee` | 兩組 `.marquee__group` 內容必須完全一樣，跑馬燈才會無縫 |
| `#about` | 側欄資訊卡（`.avatar` 的字母）與自我介紹 |
| `#skills` | 四張卡，各自的 `--hue` 決定配色 |
| `#projects` | 三張 `.card`，`href` 目前都指到 GitHub 個人頁，有個別 repo 網址可以換成各自的連結 |
| `#experience` | `.job` 時間軸，最新的放最上面 |
| `#contact` | Email、GitHub、LinkedIn、電話（`tel:` 連結） |

配色集中在 CSS 最上方的 `:root`：改 `--indigo` / `--violet` / `--rose` 就能換整站色調，
`--grad` 是主漸層。

## 部署到 GitHub Pages

推上 GitHub 後，到 repo 的 **Settings → Pages**，Source 選 `Deploy from a branch`，
branch 選 `main` / `(root)`，等一兩分鐘就會有網址。
