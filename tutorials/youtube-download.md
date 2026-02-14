---
title: "YouTube 高強度防護下載指南"
sidebarTitle: "YouTube 下載指南"
description: "如何突破 YouTube BotGuard 下載影片的完整 SOP。"
---

> **這份文件記錄了如何突破 YouTube "BotGuard" 高等級防護 (連 Downie 都可能失敗的情況)。**
> **驗證狀態 (2026/01/30)**：本系統於今日 11:02 AM 成功下載了 `Mrs Wang Sharing` 影片 (368MB)，證明以下技術路徑有效且穩定。

## 1. 核心原理 (Why it works)

傳統下載器失敗的原因是 YouTube 的 "BotGuard" 反爬蟲機制。
這套 **"The Golden Method"** 之所以成功，是因為它結合了三層防護突破：
1.  **身份借用 (Identity Theft)**：直接讀取本機 Chrome 的 `Cookies`，偽裝成「已登入的 VIP 真人」。
2.  **動態驗證 (Remote Solver)**：掛載 `ejs:github` 組件，在本機執行 YouTube 的混淆 JavaScript 驗證碼。
3.  **TLS 偽裝**: `yt-dlp` 的現代版本能模擬常見瀏覽器的 TLS 指紋。

---

## 2. 操作指令 (The Golden Command)

請在終端機 (Terminal) 執行以下指令：

```bash
# 1. 確保使用最新的 Python 3.12 (環境隔離)
# 2. 確保使用 git master 版的 yt-dlp (Bleeding Edge)
# 3. 確保 Chrome 已登入 YouTube

uv run --python 3.12 yt-dlp \
  --cookies-from-browser chrome \
  --remote-components ejs:github \
  -f "bestvideo+bestaudio" \
  --merge-output-format mp4 \
  "你的影片網址"
```

### 必備參數詳解
*   `--cookies-from-browser chrome`: **(核心)** 繞過 403 Forbidden 的關鍵。
    *   *注意：執行時 MacOS 可能彈窗詢問「Chrome Safe Storage」存取權限，請務必點擊「允許」。*
*   `--remote-components ejs:github`: **(核心)** 自動下載解密腳本，解決 "n-parameter" 限速與 403。

---

## 3. 關於 2026/01/30 11:02 的成功案例

用戶確認，今日早上 11:02 成功下載的 `02.COE 4 & TE Platinum Mrs Wang sharing 22/01/26.mp4` 檔案，正是由此技術流程完成。
這驗證了：**只要配置正確，Python 腳本完全能擊敗商業軟體 (如 Downie) 的下載能力。**

---

## 4. 自動化 Python 函式

將此函式整合到您的工具庫中，即可一鍵下載：

```python
def download_secure_video(url, output_name="video.mp4"):
    import subprocess
    cmd = [
        "uv", "run", "--python", "3.12", "yt-dlp",
        "--cookies-from-browser", "chrome",
        "--remote-components", "ejs:github",
        "-f", "bestvideo+bestaudio/best",
        "--merge-output-format", "mp4",
        "-o", output_name,
        url
    ]
    print(f"🚀 啟動防護突破下載: {url}")
    subprocess.run(cmd, check=True)
```
