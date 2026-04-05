# 土手製陶 網站內容編輯說明

本文件說明如何新增文章分類與文章頁面。

---

## 一、新增文章分類

文章分類由 `public/category.json` 統一管理，網站的 Navbar 下拉選單與首頁卡片皆會自動讀取。

**Step 1** — 開啟 `public/category.json`

**Step 2** — 在陣列末尾新增一筆資料，格式如下：

```json
{
  "id": "fen-lei-id",
  "name": "分類名稱",
  "description": "分類的簡短說明文字",
  "icon": "shelf",
  "iconUrl": "images/你的分類圖示檔名.jpg"
}
```

| 欄位 | 說明 |
|---|---|
| `id` | 英文或拼音，不可有空格，例如 `chuan-xi`，此為網址的一部分 |
| `name` | 顯示於畫面上的分類名稱 |
| `description` | 首頁卡片下方的說明文字 |
| `iconUrl` | 分類圖示圖片路徑，圖片請放入 `public/images/` 資料夾 |

**Step 3** — 將分類圖示圖片放入 `public/images/` 資料夾

**Step 4** — 執行以下指令重新部署：

```bash
git add public/category.json public/images/
git commit -m "feat: 新增分類 xxx"
git push
```

等 GitHub Actions 跑完（約 1~2 分鐘），網站即會顯示新分類。

---

## 二、新增文章

文章清單由 `public/articleList.json` 管理，文章內容為獨立的 HTML 檔案，放於 `public/articles/` 資料夾。

### Step 1 — 準備文章 HTML 檔案

複製 `public/articles/article-001.html`，將檔案重新命名，例如 `article-006.html`。

開啟檔案，修改以下內容：

- `<title>` 標籤內的文章標題
- `.category-tag` 的分類名稱
- `<h1 class="article-title">` 的文章標題
- `.meta` 的日期
- `.content` 內的文章內文（每段落用 `<p>` 包覆）

> 若有文章封面圖，將 `.thumbnail` 內的佔位文字換成 `<img>` 標籤，圖片放入 `public/images/`。

### Step 2 — 在 `articleList.json` 新增一筆資料

開啟 `public/articleList.json`，在陣列末尾新增：

```json
{
  "id": "article-006",
  "categoryId": "chuan-xi",
  "title": "文章標題",
  "content": "文章前段摘要，約100字，清單頁會自動截斷顯示...",
  "date": "2026-04-05",
  "thumbnail": "images/article-006-thumbnail.jpg",
  "htmlFile": "articles/article-006.html"
}
```

| 欄位 | 說明 |
|---|---|
| `id` | 唯一識別碼，不可重複 |
| `categoryId` | 對應 `category.json` 中的 `id`，決定文章屬於哪個分類 |
| `title` | 文章標題，顯示於清單卡片 |
| `content` | 文章摘要，清單頁顯示前 100 字，請填入文章開頭段落 |
| `date` | 格式為 `YYYY-MM-DD` |
| `thumbnail` | 縮圖路徑，圖片放入 `public/images/`；若無圖片可填 `images/placeholder.jpg` |
| `htmlFile` | 對應的 HTML 檔案路徑，即 Step 1 建立的檔案 |

### Step 3 — 部署

```bash
git add public/articles/article-006.html public/articleList.json public/images/
git commit -m "feat: 新增文章 article-006"
git push
```

等 GitHub Actions 跑完，文章即會出現於對應分類的清單頁，點擊 Read More 即可跳轉至文章頁面。

