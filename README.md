# 🌲 Haibara's Digital Garden

歡迎來到我的數位花園！這是我分享**所學、所思與技術筆記**的角落。

🔗 訪問我的網站：[https://haibara-hsu.github.io/learn/](https://haibara-hsu.github.io/learn/)

---

## 🚀 關於這個網站

這個網站是基於 **Quartz v4** 構建的。Quartz 是一個強大的工具集，能將 Markdown 筆記（如 Obsidian）轉換為快速、美觀且具備互動性的網路頁面，非常適合用於「聯網思考」（Networked Thought）的實踐。

> 「那些敞開大門工作的人，雖然會遇到各種干擾，但偶爾也能獲得關於這個世界、以及什麼才是重要的線索。」 — Richard Hamming

### 核心架構

* **引擎**: [Quartz v4](https://quartz.jzhao.xyz/)
* **部署**: GitHub Pages
* **內容**: 以 Markdown 編寫的個人知識庫

---

## 🛠️ 工作流與更新手冊

為了確保內容同步，請在本地終端機（Terminal）執行以下指令進行更新。

### 1. 進入專案目錄

```bash
cd /Users/bjhsue/quartz

```

### 2. 同步內容 (推薦方式)

使用 Quartz 內建的同步工具，這會自動處理建置與推送：

```bash
npx quartz sync --no-pull

```

### 3. 手動推送 (備用方案)

如果上述自動同步失敗，請使用標準 Git 指令推送至 `v4` 分支：

```bash
git add .
git commit -m "update notes: $(date +'%Y-%m-%d %H:%M')"
git push origin v4

```

---

## 📂 資料夾結構概覽

* `content/`: 存放所有的 Markdown 筆記與圖片（這是主要編輯區）。
* `quartz/`: Quartz 的核心配置與元件。
* `quartz.config.ts`: 網站全域設定（標題、佈景主題顏色等）。
* `quartz.layout.ts`: 頁面佈局設定。

---

## 📬 聯絡與社群

如果你對內容有任何想法或建議，歡迎透過 GitHub 聯繫我。

* **Quartz 官方文檔**: [Documentation](https://quartz.jzhao.xyz/)
* **Quartz Discord**: [Join Community](https://discord.gg/cRFFHYye7t)
