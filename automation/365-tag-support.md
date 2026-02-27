---
title: "365 挑戰標籤支援 (Tag Support)"
description: "自動化系統如何智慧處理並同步 Hashtag 至 WordPress 與社群平台"
---

## 🏷️ 功能概述

在 365 攝影挑戰的自動化流程中，**標籤 (Tags)** 是連接內容與讀者的關鍵。我們的系統 (`publish_365.py`) 內建了強大的標籤處理引擎，能自動將您在 Markdown 日記中寫的 `#Hashtag` 轉換為 WordPress 的原生標籤，並同步至社群平台。

---

## ⚙️ 運作邏輯

### 1. 自動提取 (Extraction)
系統會掃描 Markdown 檔案中的內文，尋找所有以 `#` 開頭的關鍵字。

- **輸入**: `今天天氣真好！ #陽光 #攝影 #DailyLife`
- **提取結果**: `['陽光', '攝影', 'DailyLife']`

### 2. WordPress 同步 (Sync)
提取出的標籤會與 WordPress 資料庫進行比對：
- **既有標籤**: 直接取得 ID 並連結至文章。
- **新標籤**: 若標籤不存在，系統會透過 API **自動建立**新標籤，無須手動新增。

### 3. 強制標籤 (Force Tags)
為了確保 365 挑戰系列的完整性，系統會強制為每篇文章加入以下核心標籤：
- `#365攝影挑戰`
- `#365Project`
- `#PhotoADay`

---

## 📝 寫作範例

您只需要在原本的日記中自然地加入 Hashtag 即可：

```markdown
# 365攝影挑戰 Day 100

今天去山上拍了雲海，景色真的很壯觀。

#雲海 #風景攝影 #登山 #SonyAlpha
```

**自動化系統會將這篇文章發布為：**
- **標題**: 365攝影挑戰 Day 100
- **分類**: 365 攝影挑戰
- **標籤**: 雲海, 風景攝影, 登山, SonyAlpha, 365攝影挑戰, 365Project...

---

## 🔧 技術參數

若您需要開發者級別的調整，可參考 `scripts/publish_365.py` 中的 `extract_tags` 函數：

```python
def extract_tags(content):
    # 使用 Regex 提取 #後面的文字
    return re.findall(r"#(\w+)", content)
```

目前系統已針對中文、英文與數字混合的標籤進行優化，確保各種格式都能正確識別。
