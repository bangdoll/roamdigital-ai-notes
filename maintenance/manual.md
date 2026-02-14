---
title: "網站維護手冊 (SOP)"
sidebarTitle: "維護手冊"
description: "RoamDigital AI Notes 的日常操作與維護指南。"
---

這份文件說明如何維護與更新您的「數位第二大腦」網站 `https://notes.rd.coach`。
本系統基於 **Mintlify** 構建，透過 **GitHub** 進行版本控制與自動部署 (GitOps)。

## 1. 系統架構

*   **本地專案位置**: `~/Projects/00.AI-Notes_Local/mintlify_docs`
*   **雲端網址**: [https://notes.rd.coach](https://notes.rd.coach)
*   **GitHub Repo**: [bangdoll/roamdigital-ai-notes](https://github.com/bangdoll/roamdigital-ai-notes)
*   **核心技術**: Mintlify (Docs-as-Code) + Git

---

## 2. 日常操作流程 (SOP)

### 步驟一：新增或編輯文章 📝

進入專案目錄：
```bash
cd ~/Projects/00.AI-Notes_Local/mintlify_docs
```

在 `tutorials` 或 `automation` 資料夾中新增 `.md` 檔案（或建立新資料夾）。
**注意：每篇文章必須包含 Frontmatter**（檔案最上方）：

```markdown
---
title: "文章標題"
sidebarTitle: "側邊欄標題 (可選)"
description: "簡短描述文章內容。"
---
```

### 步驟二：更新導航選單 (若為新文章) 🗺️

編輯 `mint.json`，將新檔案的路徑加入 `navigation`：

```json
"navigation": [
    {
        "group": "教學文件",
        "pages": [
            "tutorials/rubiks-cube",
            "tutorials/new-article"  <-- 新增這一行 (不用加 .md)
        ]
    }
]
```

### 步驟三：本地預覽 (Preview) 👀

在終端機執行：
```bash
mintlify dev
```
打開瀏覽器訪問 `http://localhost:3000`，確認內容無誤。

### 步驟四：發布上線 (Deploy) 🚀

只要推送到 GitHub，Mintlify 就會自動部署。

```bash
git add .
git commit -m "新增文章: [文章名稱]"
git push
```
等待約 30 秒，雲端網站 `https://notes.rd.coach` 就會自動更新。

---

## 3. 進階語法參考 (Mintlify Components)

Mintlify 支援標準 Markdown，也提供了一些增強元件：

### 提示框 (Callouts)
```markdown
<Tip>這是提示內容</Tip>
<Warning>這是警告內容</Warning>
<Note>這是備註內容</Note>
```

### 程式碼區塊 (Code Blocks)
```markdown
```python helloworld.py
print("Hello World")
```
```

### 步驟條 (Steps)
```markdown
<Steps>
  <Step title="第一步">
    說明第一步要做什麼。
  </Step>
  <Step title="第二步">
    說明第二步要做什麼。
  </Step>
</Steps>
```

### 卡片 (Cards)
```markdown
<CardGroup cols={2}>
  <Card title="魔術方塊教學" icon="cube" href="/tutorials/rubiks-cube">
    七步驟還原法
  </Card>
  <Card title="YouTube 下載" icon="video" href="/tutorials/youtube-download">
    突破 BotGuard 防護
  </Card>
</CardGroup>
```

---

## 4. 常見問題

**Q: 我修改了 `mint.json` 但左側選單沒變？**
A: `mintlify dev` 有時對設定檔變更反應較慢，請按 `Ctrl+C` 停止並重新執行 `mintlify dev`。

**Q: 圖片要放哪裡？**
A: 建議在 `mintlify_docs` 下建立 `images` 資料夾，然後用 `![Alt](/images/pic.png)` 引用。

**Q: 如何備份網站？**
A: 因為所有內容都在 GitHub 上，只要 GitHub 不倒，您的網站就永遠有備份。
