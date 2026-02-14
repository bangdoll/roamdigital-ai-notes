---
title: "AI 社交媒體助手 (PostHelper)"
description: "利用 Gemini 2.0 與 Playwright 實現自動化 AI 文案優化與臉書粉專發布"
---

<img
  className="block dark:hidden"
  src="/logo/logo.png"
  alt="PostHelper Hero"
/>
<img
  className="hidden dark:block"
  src="/logo/logo.png"
  alt="PostHelper Hero"
/>

## 📖 簡介

**PostHelper** 是一個基於 Python 的 CLI 工具，旨在幫助內容創作者利用 AI 動能提升社交媒體的影響力。它結合了 Google Gemini 的文案生成能力與 Playwright 的瀏覽器自動化技術，實現了從「想法」到「高品質發布」的一條龍流程。

### 🚀 核心優勢
- **AI 驅動**：搭載 Gemini 2.0 Flash，生成語法極其自然。
- **身分自動切換**：全台首創！自動偵測並切換 FB 臉書粉專管理員身分。
- **全平台適用**：自動適配 X、Facebook、LinkedIn、Threads 的字數與調性。
- **剪貼簿即時同步**：優化完畢即自動複製，手動貼上發布也超快。

---

## 🛠️ 使用方式

你可以在終端機透過簡單的參數來驅動這個助手。

### 1. 基礎風格優化
輸入你的初稿，選擇風格後，優化文案會自動存入你的剪貼簿。

```bash
uv run python scripts/morning_routine/post_helper.py "早安，今天也要加油喔！" --style Friendly --emoji High
```

### 2. 不同風格與平台
支援 `Professional` (專業)、`Friendly` (友善)、`Hype` (激動)、`FanPage` (粉專專用)。

```bash
# 生成專業調性的 LinkedIn 貼文
uv run python scripts/morning_routine/post_helper.py "我剛完成了一個自動化專案" --style Professional --platform LI
```

### 3. 直接發布到 Facebook 粉絲專頁
這會啟動自動化流程：**優化文案 -> 切換粉專身分 -> 上傳圖片 -> 發布內容**。

```bash
uv run python scripts/morning_routine/post_helper.py "歡迎追蹤 RoamDigitalLifeCoach！" --style FanPage --publish-fb
```

---

## 🤖 技術細節：身分切換自動化

針對 Facebook 複雜的 UI，我們設計了強大的偵測邏輯，能夠自動處理以下流程：

1. **進入粉專**：直接導航至目標連結。
2. **偵測彈窗**：主動尋找「切換個人檔案以發布內容」的提示。
3. **自動模擬點擊**：精確鎖定藍色的「切換」按鈕並執行身分切換。
4. **狀態檢查**：確保身分切換後的頁面重載完成，再執行發文動作。

---

## 📈 進階應用：Vibe Coding 實踐

這個工具是 **Vibe Coding** 的具體展現：我們不只是在寫代碼，我們在設計一種「流動感」。你可以將其整合進你的早安打卡腳本，甚至是 Telegram 機器人，讓你的數位生活更具智慧與效率。
