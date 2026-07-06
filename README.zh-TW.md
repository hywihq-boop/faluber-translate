<div align="center">
  <img src="icons/logo.png" alt="Faluber Translate" width="96" height="96" style="border-radius:18px;box-shadow:0 0 32px rgba(124,92,252,0.35)">

  # 🌐 Faluber Translate

  ### AI 智慧網頁翻譯外掛

  基於 AI 的 Chrome 瀏覽器翻譯外掛。文字節點級 DOM 操作，50 種語言，相容 OpenAI 格式 API。

  ![version](https://img.shields.io/badge/version-2.0.10-7c5cfc?style=flat-square)
  ![manifest](https://img.shields.io/badge/manifest-v3-blue?style=flat-square)
  ![license](https://img.shields.io/badge/license-MIT-green?style=flat-square)
  ![chrome](https://img.shields.io/badge/Chrome-✓-4ade80?style=flat-square)
  ![edge](https://img.shields.io/badge/Edge-✓-4ade80?style=flat-square)

  <br>

  <table align="center"><tr>
  <td align="center"><b>50+</b><br><sup>支援語言</sup></td>
  <td align="center"><b>2</b><br><sup>翻譯模式</sup></td>
  <td align="center"><b>8</b><br><sup>併發翻譯</sup></td>
  <td align="center"><b>10</b><br><sup>API 提供商</sup></td>
  <td align="center"><b>~1s</b><br><sup>詞語解釋</sup></td>
  </tr></table>

  <br>
  <a href="https://github.com/hywihq-boop/faluber-translate/releases"><img src="https://img.shields.io/badge/⬇_下載-最新版本-7c5cfc?style=for-the-badge" alt="下載"></a>
  &nbsp;
  <a href="https://github.com/hywihq-boop/faluber-translate"><img src="https://img.shields.io/badge/⭐_Star-on_GitHub-5ce0fc?style=for-the-badge" alt="Star"></a>
</div>

<br>

---

## ✨ 核心功能

<table>
<tr>
<td width="50%">

### 🚀 一鍵整頁翻譯
點擊懸浮球或按 <kbd>Alt+T</kbd> 翻譯整個頁面。文字節點級替換，不破壞頁面結構。

</td>
<td width="50%">

### 🔍 Ctrl + 智慧解釋
滑鼠指向詞彙 + 單擊 <kbd>Ctrl</kbd> 彈出 AI 解釋氣泡。選取文字 + <kbd>Ctrl</kbd> 解釋整段。零 DOM 污染。

</td>
</tr>
<tr>
<td width="50%">

### ⚡ 雙檔翻譯模式
**標準** — 3 併發，視野優先，速度與消耗均衡。<br>
**極速** — 8 併發，全頁翻譯，速度拉滿。

</td>
<td width="50%">

### 🔑 多 API 管理
內建 10 家提供商預設。儲存多個 API 設定，隨時切換。自動拉取可用模型，支援自訂介面。

</td>
</tr>
<tr>
<td width="50%">

### 📋 翻譯面板 <kbd>Alt+Q</kbd>
左右佈局的浮動翻譯面板，輸入原文即時翻譯。獨立於頁面翻譯，支援任意語言對。

</td>
<td width="50%">

### 💾 智慧快取
記憶體 + 持久化雙層快取，1 小時 TTL。重複內容不消耗 token。語言切換自動清除。

</td>
</tr>
</table>

---

## 📦 三步開始

<table>
<tr>
<td align="center" width="33%">
  <b>1. 安裝</b><br>
  <sup>從 <a href="https://github.com/hywihq-boop/faluber-translate/releases">Releases</a> 下載 zip，解壓縮後<br>在 <code>chrome://extensions</code> 載入</sup>
</td>
<td align="center" width="33%">
  <b>2. 設定 API</b><br>
  <sup>選擇提供商，填入 API Key，<br>測試連線，儲存</sup>
</td>
<td align="center" width="33%">
  <b>3. 翻譯</b><br>
  <sup>開啟任意網頁，點擊懸浮球<br>或按 <kbd>Alt+T</kbd></sup>
</td>
</tr>
</table>

---

## 🔧 10 家 API 提供商

內建預設，相容任意 OpenAI 格式 API：

| 提供商 | API 位址 |
|--------|----------|
| ⭐ DeepSeek | `https://api.deepseek.com/v1` |
| OpenAI | `https://api.openai.com/v1` |
| Groq | `https://api.groq.com/openai/v1` |
| Together AI | `https://api.together.xyz/v1` |
| OpenRouter | `https://openrouter.ai/api/v1` |
| SiliconFlow | `https://api.siliconflow.cn/v1` |
| Moonshot | `https://api.moonshot.cn/v1` |
| 智譜 | `https://open.bigmodel.cn/api/paas/v4` |
| 阿里百煉 | `https://dashscope.aliyuncs.com/compatible-mode/v1` |
| 自訂 | 任意 OpenAI 相容端點 |

---

## 🛠️ 運作原理

```
使用者觸發翻譯
  → Content Script 走訪 DOM，收集可見文字節點
  → 可見性偵測 → CJK 去重 → 最小長度過濾 → 快取去重
  → 按 Y 座標排序，相鄰節點合併
  → 分包 → 發 Service Worker（3–8 併發）
  → 調 AI API（OpenAI 相容格式）→ 返回結果
  → DOM 文字替換 → 即時進度條
```

### 智慧處理
- 跳過 `<script>`、`<style>`、`<code>` 等非內容標籤
- 過濾數字、URL、Emoji 等不可翻譯內容
- 偵測 `display:none`、`visibility:hidden` 隱藏狀態
- 保留 HTML 實體和特殊字元
- 相鄰文字節點合併後傳送

### 模式對比

| 參數 | 標準 | 極速 |
|------|------|------|
| 併發數 | 3 | 8 |
| 分批大小 | 400 字元 | 250 字元 |
| 翻譯範圍 | 僅可見區域 | 全頁 |
| 捲動偵測 | ✅ | — |
| 懸停偵測 | ✅ | — |
| 動態內容 | ✅ | ✅ |

### 快取系統
| 層級 | 儲存 | 上限 | TTL |
|------|------|------|-----|
| 記憶體 | `Map<原文, 譯文>` | 無限制 | 工作階段 |
| 持久化 | `chrome.storage.local` | 2,000 | 1 小時 |

---

## 🌍 50 種目標語言 · 20 種介面語言

<details>
<summary>展開檢視完整語言列表</summary>
<br>

`简体中文` `繁體中文` `English` `日本語` `한국어` `Français` `Deutsch` `Español` `Português` `Русский` `العربية` `हिन्दी` `ไทย` `Tiếng Việt` `Italiano` `Nederlands` `Polski` `Türkçe` `Bahasa Indonesia` `Svenska` `Dansk` `Suomi` `Norsk` `Čeština` `Română` `Magyar` `Ελληνικά` `עברית` `Українська` `Melayu` `Filipino` `বাংলা` `اردو` `فارسی` `Kiswahili` `தமிழ்` `తెలుగు` `मराठी` `ગુજરાતી` `ಕನ್ನಡ` `മലയാളം` `ਪੰਜਾਬੀ` `Български` `Slovenčina` `Lietuvių` `Latviešu` `Eesti` `Slovenščina` `Hrvatski` `Српски`

</details>

---

## 📂 專案結構

```
faluber translate/
├── manifest.json              # 擴充功能設定 (Manifest V3)
├── background/
│   └── service-worker.js      # API 呼叫與訊息路由
├── content/
│   ├── content.js             # DOM 文字擷取與替換
│   └── content.css            # 懸浮球樣式
├── popup/
│   ├── popup.html             # 設定彈窗
│   ├── popup.js               # 多 API 管理
│   └── popup.css              # 彈窗樣式
├── icons/                     # 擴充功能圖示
├── docs/                      # 產品官網
└── generate-icons.js          # 圖示產生器（開發工具）
```

---

## 🔒 隱私

- API Key 僅儲存在 Chrome **本機**同步儲存中
- 翻譯請求**直接**從瀏覽器傳送到你的 API 提供商
- **不經由第三方伺服器** — 資料只在你和 API 提供商之間傳輸

---

<div align="center">
  <br>
  <a href="https://github.com/hywihq-boop/faluber-translate">⭐ Star on GitHub</a> ·
  <a href="https://github.com/hywihq-boop/faluber-translate/releases">📦 下載</a> ·
  <a href="https://github.com/hywihq-boop/faluber-translate/issues">🐛 回報 Bug</a> ·
  <a href="LICENSE">📝 MIT 授權</a>
  <br><br>
  <sub>用 ❤️ 製作 · 不收集任何使用者資料</sub>
</div>
